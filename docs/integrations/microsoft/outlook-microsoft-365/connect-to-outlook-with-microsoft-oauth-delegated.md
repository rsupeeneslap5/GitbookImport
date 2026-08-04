---
description: >-
  This section shows how to set up a secure Outlook connection so SlapFive's
  automation engine can send emails through Microsoft Outlook using Microsoft
  365.
---

# Connect to Outlook with Microsoft OAuth (Delegated)

Microsoft Outlook uses **Authorization Code Grant (Delegated Authentication)** to enable SlapFive to connect to Outlook. This method connects to Outlook using a signed-in mailbox user. Emails can be sent:

* From the mailbox used to create the Outlook connection.
* From a shared mailbox.
* From individual employees, such as the Assigned To user on a Request.

### Prerequisites

The mailbox used to create the Outlook connection must:

* Be a licensed Exchange Online mailbox.
* Be able to sign in interactively.
* Use Multi-Factor Authentication (MFA) if required by your Microsoft 365 tenant.

### Create the Outlook Connection in SlapFive

1. In SlapFive, go to **Settings > Integrations**.
2. Open the **Outlook Connection** integration.
3. Click **Connect**.
4. Sign in using the mailbox that will authenticate the Outlook connection.
5. Complete Multi-Factor Authentication (MFA), if prompted.
6. Review and approve the Microsoft consent prompts.

> **Security Note**
>
> No usernames or passwords are stored in SlapFive. Microsoft issues OAuth access and refresh tokens, which are securely stored by the automation platform and used to authenticate future email requests.

### Sending Emails from the Connected Mailbox

The simplest configuration is to send all emails from the mailbox that authenticated the Outlook connection.

For example:

```
customer.references@company.com
```

In this configuration, all emails sent by SlapFive will appear to come from that mailbox.

No additional Exchange configuration is required.

### Sending Emails from a Shared Mailbox

Many organizations prefer to send emails from a shared mailbox such as:

```
references@company.com
advocacy@company.com
```

In this scenario:

* Connect SlapFive using a licensed user mailbox or service account.
* Grant that mailbox **Send As** permission on the shared mailbox.

For example:

```
Add-RecipientPermission `
  -Identity references@company.com `
  -Trustee customer.references@company.com `
  -AccessRights SendAs `
  -Confirm:$false
```

After the permission has been granted, SlapFive can send emails that appear to come from the shared mailbox.

### Sending Emails from Individual Employees

Some organizations prefer emails to come directly from the employee responsible for the customer, such as the Request Assigned to User or the Account Owner.

In this configuration:

* The Outlook connection continues to authenticate using a single mailbox.
* SlapFive dynamically supplies the employee's email address as the **From** address.
* The connected mailbox must have **Send As** permission for every employee mailbox that may be used as a sender.

### Configure the Send As permissions

**Send As permissions are configured by a Microsoft 365 / Exchange administrator.**

The Exchange administrator grants permission **on each employee mailbox**, allowing the mailbox connected to SlapFive to send as that employee.

#### Example

Suppose the Outlook connection was created using:

```
customer.references@company.com
```

If SlapFive needs to send email from:

```
john.smith@company.com
mary.jones@company.com
jane.doe@company.com
```

then the Exchange administrator grants **Send As** permission on each employee mailbox to:

```
customer.references@company.com
```

Example PowerShell:

```
Add-RecipientPermission `
  -Identity john.smith@company.com `
  -Trustee customer.references@company.com `
  -AccessRights SendAs `
  -Confirm:$false
```

Repeat this command for each employee mailbox that SlapFive may use as the sender.

Once configured, recipients will see the email as coming directly from the employee rather than from the connected mailbox.



















[CC-based auth](connect-to-outlook-with-with-client-credentials-based-auth.md).
