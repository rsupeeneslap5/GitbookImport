---
description: >-
  This section shows how to set up a secure Outlook connection so automated
  workflows can send emails from standard addresses such as
  references@company.com or advocacy@company.com.
---

# Connect to Outlook

## Overview

SlapFive's Automation Engine supports two methods for connecting to Outlook to send emails:

1.  **Authorization Code Grant (Delegated Authentication):**

    This method connects Outlook using **delegated authentication**, meaning emails are sent **on behalf of a signed-in mailbox user** rather than a headless application. This is by far the simpler option, and should be used unless your company has a policy stating you are not allowed to have a human user be the security principal for an automated system.
2. **Client Credentials–based authentication (OAuth 2.0)** with a **tenant-specific connection:** \
   This method allows automations to send emails from approved mailboxes without needing an individual user to sign in.

***

## Method 1: Authorization Code Grant (Delegated Authentication)

### Prerequisites

1. **A standard user mailbox exists**
   * Example: `reference@company.com` or `advocacy@company.com`
   * The mailbox must:
     * Be licensed for Exchange Online
     * Be able to sign in
     * Use MFA per tenant policy
2.  **(Optional) Shared mailbox Send As**

    * If emails should come from a shared mailbox (e.g. `references@company.com`):
      * The signed-in user must have **Send As** permission on that mailbox
      * Send As is configured on the _shared mailbox_, not the user

    Example (PowerShell):

    ```powershell
    Add-RecipientPermission `
      -Identity references@company.com `
      -Trustee mattw@company.com `
      -AccessRights SendAs `
      -Confirm:$false
    ```

### Create the Outlook Connection in SlapFive

In SlapFive, go to **Settings > Integrations** and click to open the box named **Outlook Connection** and click the **Connect** button.

1. Sign in using the chosen mailbox user.
2. Complete MFA as required.
3. Approve Microsoft consent prompts.

No passwords are shared with SlapFive.

## Method 2: Client Credentials–based authentication (OAuth 2.0)

### Prerequisites

1. Microsoft 365 tenant (Exchange Online)
2. Admin access to **Microsoft Entra ID** (formerly Azure AD)
3. Admin access to **Exchange Admin Center** or PowerShell
4. Access to your company’s **Workato workspace**

***

### Step 1. Register the App in Microsoft Entra ID

Sign into your [Azure portal](https://portal.azure.com/) and go to **Microsoft Entra ID** **>** **App registrations** **>** **New registration**.

Enter the following data and click **Register**.

1. **Name:** enter _SlapFive Email Automation_.
2. **Supported account types:** choose **Accounts in this organizational directory only (Single tenant)**.
3.  **Redirect URI**: select **Web** from the platform dropdown and enter:

    ```
    https://www.workato.com/oauth/callback
    ```

***

### Step 2. Add Microsoft Graph API Permissions

Open the new app and go to **Manage > API permissions.** Select **+ Add a permission** and select **Microsoft Graph APIs**.

1. **What type of permissions does your app require?** choose **Application permissions.**\
   &#xNAN;_(This is required for Client Credentials–based authentication.)_
2. **Select permissions:** the minimum permissions are `Mail.Send` and `Mail.Read` .
3. Click **Add permissions**.
4. Back on the **API permissions** page, click **Grant admin consent for \<your organization name>** and confirm. This approves the permissions for all users in the tenant. If this step is skipped, non-admin users who try to create the Workato Outlook connection will see a **“Need admin approval”** message and won’t be able to proceed.

***

### Step 3. Create a Client Secret

Go to **Manage > Certificates & Secrets** **> Client Secrets**, and click **+ New client secret**.

1. Give it a descriptive name, choose an expiry (12 months or longer).
2. Click **Add.**
3. Copy the secret **Value** immediately — it won’t be visible later.

***

### Step 4. Obtain the Client ID, Object ID, and Tenant ID

Go to **Overview > Essentials.** Copy and save these items:

* [ ] **Application (client) ID**
* [ ] **Object ID**
* [ ] **Directory (tenant) ID**

***

### **Step 5. Verify the mailbox exists and is mail-enabled**

Before continuing, confirm that the email address you plan to send from (for example, `references@company.com`) exists as a mailbox in Exchange Online. This step prevents common “403 Forbidden” errors when sending email.

**How to verify:**

Option A — Exchange Admin Center

* Go to **Exchange Admin Center → Recipients → Mailboxes**
* Confirm the mailbox appears in the list
* Confirm it is either:
  * A **User mailbox** with an Exchange Online license, or
  * A **Shared mailbox** (mail-enabled)

Option B — PowerShell (recommended for admins)\
Run the following command:

```powershell
Get-Mailbox references@company.com
```

If the command returns no result or an error, the mailbox is not available to Microsoft Graph and cannot be used.

**Important notes:**

* Entra ID users without Exchange mailboxes cannot send email
* Shared mailboxes must be mail-enabled
* Aliases and distribution lists are not valid sender mailboxes

Only continue once the mailbox is confirmed.

### Step 6. Obtain the User ID (User Principal Name)

Workato requires a “User ID” to identify the default mailbox the app will act on.\
This does **not** authenticate a user — it simply tells Microsoft Graph which mailbox to use.

The User ID must be the **primary SMTP email address** of a mailbox that exists in Exchange Online and is authorized for sending.

Examples:

* ✅ `references@company.com` (user mailbox or shared mailbox)
* ❌ Distribution lists
* ❌ Mail contacts
* ❌ Aliases that are not the primary SMTP address

The mailbox specified here must also be included in the Exchange **Application Access Policy** configured in Step 7.

Go to **Microsoft Entra ID >** **Users** and search for the mailbox you want the connection to send from (i.e. `references@company.com`).

Copy the **User Principal Name** (which will usually be the same as the mailbox’s email address). You’ll enter this value later in SlapFive as the **User ID** or **Default user**.

***

### Step 7. Authorize the App to send from mailboxes

Create an **Application Access Policy** in Exchange Online that allows your app to send mail from specific mailboxes (shared or regular).

1. Create a mail-enabled security group.&#x20;
   1. Name it something like _SlapFive Email Senders_.
   2. Add every mailbox (`references@company.com`, `advocacy@company.com`, etc.) that the app should be allowed to send from.
2. Run these PowerShell commands:

```
Connect-ExchangeOnline -UserPrincipalName <admin@domain.com>
New-ApplicationAccessPolicy -AppId <CLIENT_ID> `
  -PolicyScopeGroupId "SlapFive Email Senders" `
  -AccessRight RestrictAccess `
  -Description "Allow SlapFive Email Automation to send as approved mailboxes"
```

Verify the policy:

```
Get-ApplicationAccessPolicy | fl
```

Wait at least 30 minutes after creating or modifying the Application Access Policy before creating the Outlook Connection in Step 7, to allow time for Exchange to propogate the changes.

***

### Step 8. Create the Outlook Connection in SlapFive

In SlapFive, go to **Settings > Integrations** and click to open the box named **Outlook Connection**. Enter this information and click the **Connect** button.

* [ ] **Connection account type**: select **Tenant-specific**.
* [ ] **Tenant ID/Domain:** paste the **Directory (tenant) ID** from Step 4.
* [ ] **Authentication type:** select **Client Credentials**.
* [ ] **User ID:** paste the the **User Principal Name** from Step 6.
* [ ] **Client ID:** paste the **Application (client) ID** from Step 4.
* [ ] **Client secret:** paste the secret **Value** from Step 3.

Repeat this step for each standard mailbox you’ll use (i.e.  `advocacy@company.com`) using the same Tenant ID, Client ID, and Client secret but different **Default user** values.

### Troubleshooting the Outlook Connection

**Error: 403 Forbidden when sending email**

If the Outlook connection succeeds but sending email fails with a 403 error, check the following:

* The Microsoft Graph API Permissions DO NOT include `offline_access`
* The sender email address exists as a mailbox in Exchange Online
* The mailbox is included in the Application Access Policy group
* The policy has had at least 30 minutes to propagate
* The User ID exactly matches the mailbox’s primary SMTP address
