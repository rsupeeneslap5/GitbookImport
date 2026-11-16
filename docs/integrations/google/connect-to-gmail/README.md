---
description: >-
  This section covers how to establish your Gmail Connection within SlapFive's
  Embedded Integration so you can send emails from Gmail.
---

# Connect to Gmail

The Gmail connection must be authenticated using a **Google Workspace Gmail account that can sign in to Gmail**. You cannot authenticate the connection using an alias, Google Group, collaborative inbox, or other shared address that does not have its own Gmail account.

You can, however, **send emails from an alias or Google Group address** if that address is configured as a **Send mail as** address for the Gmail account used to connect SlapFive.

For example, if you want SlapFive to send from [**references@mycompany.com**](mailto:references@mycompany.com), use one of these methods:

1. **Dedicated Gmail account:** If `references@mycompany.com` is a Google Workspace Gmail account with its own login, connect SlapFive using that account. This is the preferred method.
2. **Alias or Google Group:** If `references@mycompany.com` is an alias, Google Group, or other shared address without its own Gmail login, connect SlapFive using a corporate Gmail account that has been configured to **Send mail as** `references@mycompany.com`. Then follow the Send emails from an Alias instructions below.

### **Connect SlapFive to Gmail**

Go to **SlapFive Settings → Integrations**.&#x20;

* [ ] Click on the Gmail connection you need to connect.
* [ ] Leave the connection settings at their default values and click **Sign in with Google**.
* [ ] Select the Google Workspace Account you want SlapFive to use:
  * [ ] For a dedicated Gmail account, select that account.
  * [ ] For an alias or Google Group, select the corporate Gmail account that has permission to **Send mail as** the shared address.
* [ ] When Google tells you that Workato will access your Google account, click **Continue**.
* [ ] Review the requested permissions and click **Allow**.
* [ ] After the connection completes, you will return to SlapFive Settings > Integrations. The connection should display **Disconnect** and a green <mark style="color:green;">**Connection success**</mark> message.

### Grant the Workato OAuth app access to Google services

Your Google Workspace Admin may need to authorize the Workato OAuth app for your domain.

1. Go to the **Google Admin Console**.
2. Select **Security → API Controls → App Access Control**.
3. Find the Workato OAuth app under **Configured apps**. It may appear as **Workato** or **Workato Gmail Connector**.
4. Click **Change Access**.
5. Select **Trusted: Can access all Google services**.
6. Save your changes.

The Workato OAuth app will typically appear after a user in your Google Workspace domain has attempted to connect Gmail from SlapFive.

### Verify Access to Gmail API Scopes

In the Workato app details in the Google Admin Console:

1. Review the requested OAuth scopes.
2. Confirm that the following Gmail scope is included:\
   `https://www.googleapis.com/auth/gmail.send`
3. Make sure the scope is not blocked and that the app is permitted to access Gmail for your domain.

### Send emails from an Alias or Google Group

Follow these additional steps if you want SlapFive to send from an address that does not have its own Gmail login, such as `references@mycompany.com`.

#### Add the Shared Address to Your Gmail Account

The shared address must appear as a **Send mail as** identity in the Gmail account connected to SlapFive.

1. Sign in to Gmail using the corporate account you connected to SlapFive.
2. Click **Settings → See all settings**.
3. Open the **Accounts** tab.
4. Under **Send mail as**, click **Add another email address**.
5. Enter the shared email address, such as `references@mycompany.com`.
6. Complete Google's verification process.
7. Confirm that the shared address appears under **Send mail as**.

#### If the Address Is a Google Group

If the shared address is a Google Group, your Google Workspace Admin may also need to allow you to send as the group.

1. Open the group in the Google Admin Console.
2. Review the group's posting permissions.
3. Make sure your account is permitted to post or send as the group.
4. Save any changes.

#### Verify Sending from Gmail

Before using the address in SlapFive, test it directly in Gmail:

1. Compose a new email.
2. Select the shared address in the **From** field.
3. Send a test message.

If Gmail can successfully send the message using the shared address, SlapFive can use that address when sending through the connected Gmail account.

#### Reconnect Gmail if Necessary

If you added or changed the **Send mail as** configuration after connecting Gmail to SlapFive, reconnecting the Gmail connection can refresh its authorization:

1. Go to **SlapFive Settings → Integrations**.
2. Open the Gmail connection.
3. Click **Disconnect**.
4. Click **Connect** and authenticate again using the same corporate Gmail account.
