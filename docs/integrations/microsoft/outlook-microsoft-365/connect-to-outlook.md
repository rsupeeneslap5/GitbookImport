---
description: >-
  This section shows how to set up a secure Outlook connection so automated
  workflows can send emails from standard addresses such as
  references@company.com or advocacy@company.com.
---

# Connect to Outlook

Microsoft Outlook uses **Authorization Code Grant (Delegated Authentication)** for enabling SlapFive's automation engine to connect to Outlook to send emails. This method connects to Outlook using **delegated authentication**, meaning emails are sent **on behalf of a signed-in mailbox user.**

### Prerequisites

1. **A standard user mailbox exists**
   * Example: `reference@company.com` or `advocacy@company.com`
   * The mailbox must:
     * Be licensed for Exchange Online
     * Be able to sign in
     * Use MFA per tenant policy
2.  **(Optional) Shared mailbox Send As**

    * If emails should come from a shared mailbox (e.g. `references@company.com`):
      * Connect with a service account that has **Send As** permission on the shared mailbox.
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

1. Sign in using the chosen mailbox user (or service account).
2. Complete MFA as required.
3. Approve Microsoft consent prompts.

No passwords are shared with SlapFive.





























[CC-based auth](connect-to-outlook-with-client-credentials-based-auth.md).
