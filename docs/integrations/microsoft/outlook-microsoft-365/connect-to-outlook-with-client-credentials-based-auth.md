---
description: >-
  This section shows how to set up Client Credentials-based authentication so
  automated workflows can send emails from standard addresses such as
  references@company.com or advocacy@company.com.
hidden: true
---

# Connect to Outlook with Client Credentials-based auth

### Prerequisites

1. Microsoft 365 tenant (Exchange Online)
2. Admin access to **Microsoft Entra ID** (formerly Azure AD)
3. Admin access to **Exchange Admin Center** or PowerShell
4. Access to your **SlapFive Client Settings**

***

### Step 1. Register the App in Microsoft Entra ID

Sign into your [Azure portal](https://portal.azure.com/) and go to **Microsoft Entra ID** **>** **App registrations** **>** **New registration**.

Enter the following data and click **Register**.

1. **Name:** enter _SlapFive Email Automation_.
2. **Supported account types:** choose **Accounts in this organizational directory only (Single tenant)**.
3. **Redirect URI**: leave blank and don't select a Platform.

***

### Step 2. Add Microsoft Graph API Permissions

Open the new app and go to **Manage > API permissions.** Select **+ Add a permission** and select **Microsoft Graph APIs**.

1. **What type of permissions does your app require?** choose **Application permissions.**\
   &#xNAN;_(This is required for Client Credentials–based authentication.)_
2. **Select permissions:** the minimum permissions are `Mail.Send`  and  `Mail.ReadWrite` .
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

You will need to collect two different Object IDs from two different places in Entra ID — one from the App Registration and one from the Enterprise Application. These are different objects and should not be confused with each other.

**From the App Registration:**

Go to **Microsoft Entra ID > App registrations > SlapFive Email Automation > Overview > Essentials** and copy:

* **Application (client) ID**
* **Directory (tenant) ID**

**From the Enterprise Application:**

Go to **Microsoft Entra ID > Enterprise applications**, search for _SlapFive Email Automation_, and open it. From the **Overview** page, copy:

* **Object ID** (this is the Enterprise Application Object ID, which is required for Step 7)

Save all three values — you will need them in later steps.

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

The mailbox specified here must also be a member of the **mail-enabled security group** configured in Step 7.

Go to **Microsoft Entra ID >** **Users** and search for the mailbox you want the connection to send from (i.e. `references@company.com`).

Copy the **User Principal Name** (which will usually be the same as the mailbox’s email address). You’ll enter this value later in SlapFive as the **User ID** or **Default user**.

***

### Step 7. Authorize the App to Send from Mailboxes

Grant the app permission to send from specific mailboxes using Exchange Online's Role Based Access Control (RBAC) for Applications.

**Create a mail-enabled security group.**

Name it something like _SlapFive Email Senders_ and add every mailbox the app should be allowed to send from (e.g. [references@company.com](mailto:references@company.com), [advocacy@company.com](mailto:advocacy@company.com)).

**Register the app as a Service Principal in Exchange Online.**

Run the following PowerShell commands, using the Application (client) ID and Enterprise Application Object ID from Step 4:

```powershell
powershell

Connect-ExchangeOnline -UserPrincipalName <admin@domain.com>

New-ServicePrincipal `
    -AppId <CLIENT_ID> `
    -ObjectId <ENTERPRISE_APP_OBJECT_ID>
```

**Create a Management Scope for the security group.**

```powershell
powershell

New-ManagementScope `
    -Name "SlapFive Email Senders Scope" `
    -RecipientRestrictionFilter "MemberOfGroup -eq '<group email address>'"
```

**Assign the Mail.Send role to the app.**

```powershell
powershell

New-ManagementRoleAssignment `
    -Name "SlapFive Mail.Send" `
    -Role "Application Mail.Send" `
    -App <CLIENT_ID> `
    -CustomResourceScope "SlapFive Email Senders Scope"
```

**Verify the assignment.**

```powershell
powershell

Test-ServicePrincipalAuthorization `
    -Identity <CLIENT_ID> `
    -Resource references@company.com
```

The result should show `InScope = True` for the mailbox. If it returns `False`, confirm the mailbox is a member of the security group and wait a few minutes for changes to propagate.

Wait at least 60 minutes after completing this step before creating the Outlook Connection in Step 8, to allow Exchange time to propagate the changes.

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

**Error: `New-ServicePrincipal` fails in Step 7**

The Service Principal may already exist in Exchange Online if the app was previously registered. Try running `Get-ServicePrincipal -AppId <CLIENT_ID>` first. If it returns a result, skip the `New-ServicePrincipal` command and proceed.

**Error: `New-ManagementScope` fails with a filter error**

The `MemberOfGroup` filter requires the group's distinguished name (DN), not always its email address. If the command fails, retrieve the DN first with:

```powershell
powershell

Get-Group "SlapFive Email Senders" | Format-List DistinguishedName
```

Then use the DN value in the filter instead of the email address.

**Error: Connection succees but 403 Forbidden error received when sending email**

If the Outlook connection succeeds but sending email fails with a 403 error, check the following:

* The sender email address exists as a mailbox in Exchange Online
* The mailbox is a member of the SlapFive Email Senders security group configured in Step 7
* The policy has had at least 60 minutes to propagate
* The User ID exactly matches the mailbox’s primary SMTP address

**Connection succeeds but emails arrive from the wrong address**

If email is sent from a different address than expected, the User ID entered in Step 8 may not exactly match the mailbox's primary SMTP address. Verify by running `Get-Mailbox <address> | Format-List PrimarySmtpAddress` and confirm it matches what was entered as the User ID.

**Client secret expiry**

If the connection stops working after 12 months, the client secret has likely expired. Return to Step 3, create a new secret, and update the Client secret value in the SlapFive Outlook Connection settings.
