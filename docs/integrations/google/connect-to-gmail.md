---
description: >-
  This section covers how to establish your Gmail Connection within SlapFive's
  Embedded Integration so you can send emails from Gmail.
---

# Connect to Gmail

SlapFive's Embedded Integration and Automation module allows you to send emails from any Google Workspace business Gmail account that belongs to your corporate domain. You cannot send directly from an Alias, a Google Group, a collaborative inbox, a shared mailbox that is not a Gmail account with a username and password, or a personal Gmail account.

Since most SlapFive users want to send from a shared email address like **references@mycompany.com** or **customers@mycompany.com**, there are two methods you can use to set it up:

1. If the shared email address is a Gmail account that has a direct login with username and password, connect to Gmail using that Gmail account. (Preferred)
2. If the shared email address is an Alias and not a full Gmail account, connect to Gmail using any corporate Gmail account and follow the additional steps below for [Send emails from an Alias](connect-to-gmail.md#send-emails-from-an-alias).

For both methods, do the following:

### **Connect SlapFive to Gmail**

* [ ] Go to **SlapFive Settings → Integrations**.&#x20;
* [ ] Click on the name of the Gmail connection you need to connect.
* [ ] Leave everything set to default values and click the **Sign in with Google** button.
* [ ] On the Sign in with Google screen, select the Google Account for the shared email address' Gmail Account if you're using method 1, or your own corporate Gmail account if you're using method 2.
* [ ] On the next screen, Google tells you that Workato will access your Google account, click **Continue**.
* [ ] On the final screen, Google tells you what permissions will be shared, click **Allow**.
* [ ] Once you are successfully connected, you are taken back to the SlapFive Integrations tab screen and the button should now say **Disconnect**, and you should see a green <mark style="color:green;">**Connection success**</mark> message.

### Grant the Workato OAuth app access to Google services

Have your Google Workspace Admin do the following:

* [ ] Go to [https://admin.google.com](https://admin.google.com).
* [ ] In the left navigation, select **Security → API Controls → App Access Control**.
* [ ] Find and click the Workato OAuth app, which will appear as an OAuth app after any user in your Google Workspace domain has attempted a Gmail connection using a corporate Gmail account. Connecting with a personal Gmail account or an alias will NOT make the OAuth app appear. You will find it by looking under Configured apps for Workato or Workato Gmail Connector.&#x20;
* [ ] Click **Change Access**.
* [ ] Choose **Trusted: Can access all Google services**. Gmail blocks sending unless the OAuth app is explicitly trusted at the domain level.
* [ ] Save your changes.

### Verify Access to Gmail API Scopes

* [ ] Inside the app detail page, review the list of requested scopes, and make sure it includes:
  * `https://www.googleapis.com/auth/gmail.send`
* [ ] Make sure none are blocked.
* [ ] Confirm the app is permitted to use Gmail scopes for the domain.

### **Send emails from an Alias**

Do these additional steps only for method 2, where you plan to send emails from an Alias or shared inbox:

#### **Add the Alias to Your Gmail Account**

You must add the shared email address as a “Send mail as” identity under your own Gmail account.

* [ ] Log into Gmail with your corporate account.
* [ ] Click the gear icon → **See all settings**.
* [ ] Go to the **Accounts** tab.
* [ ] In the **Send mail as:** section, click **Add another email address**.
* [ ] Enter the shared email address (e.g., references@yourcompany.com).
* [ ] When asked how you want to send mail, choose: **Send through Gmail (easier to set up).** Do not choose the option to send through an external SMTP server. Workato cannot use external SMTP configurations.
* [ ] Gmail will send a verification email to the shared address. Depending on how it is configured, it may forward to individual users or to your IT admin.
* [ ] Enter the verification code to complete setup.
* [ ] Confirm the alias now appears in the “Send mail as” list with a **Verified** label.

If you do not see the shared address as Verified, Gmail will not allow Workato to send as it.

#### **Make Sure You Have Permission to “Send As” the Alias**

Your Google Workspace Admin must confirm you are allowed to send emails as the shared address:

* [ ] Open **Google Groups** in the Admin Console.
* [ ] Click the group (e.g., references@yourcompany.com).
* [ ] Go to **Permissions** → **Posting permissions**.
* [ ] Set **Who can post as the group?** to include **your user account**. If you skip this step, Gmail will accept the alias into your **Send mail as** list but will block mail sending with a 403 error.
* [ ] Click the **Sav**e button.

This tells Google: “This user is allowed to send email as this shared address.”

#### **Verify That Gmail Recognizes You as an Approved Sender**

Back in your own Gmail settings:

* [ ] Refresh Gmail.
* [ ] Go back to Settings → Accounts → **Send mail as**.
* [ ] Confirm that the shared email address:
  * appears in your list
  * shows **Verified**
  * does **not** show “Error,” “Verification needed,” or “Permission denied”

If it’s Verified here, Gmail will allow the SlapFive integration server (Workato) to send from that address on your behalf.

#### **Reconnect Your Gmail Connection in SlapFive**

Once the alias is verified and permissions are set:

* [ ] Go to **SlapFive Settings → Integrations**.
* [ ] Click your Gmail connection.
* [ ] Click **Disconnect**.
* [ ] Click **Connect** again and authenticate with your own corporate Gmail address.

This ensures Google refreshes the permission set and SlapFive receives Gmail’s updated list of approved sender identities.
