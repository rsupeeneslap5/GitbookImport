---
description: >-
  This section covers how to establish your Sharepoiint Connection within
  SlapFive's Embedded Integration.
---

# Connect to Sharepoint

To protect the security and privacy of your Sharepoint data, SlapFive's Embedded Integration eliminates the need for you to email or message us with your Client Key or Client Secret. You or your Microsoft Admin can simply connect right from within SlapFive. You only have to do this once and it will be used for all Sharepoint integration and data synchronization scenarios. The login data is then encrypted and stored within the Embedded Integration.

1\. In SlapFive, go into **Settings**, and click on the **Integrations** sub-tab.

2\. Click the **Sharepoint Connection** box to expand it. Enter the following fields and click **Connect**.

* [ ] **Subdomain:** Enter the subdomain from your SharePoint URL. For example, if your SharePoint URL is `https://abc.sharepoint.com`, enter `abc`.
* [ ] **Client ID:** Paste the Client ID from your SharePoint app registration. Click the "learn how to generate Client ID" link on the connection screen for instructions on how to get this ID.
* [ ] **Client Secret:** Paste the Client Secret associated with your app registration. Click the "learn how to generate Client secret" link on the connection screen for instructions on how to get this ID.
* [ ] **Site Name** _(optional)_ — The name of the specific SharePoint site you want to connect to. Leave this blank to connect to your default home site. If you only have access to a specific site, find its name in the URL: for example, if the URL is `https://company-name.sharepoint.com/sites/product`, enter `product`.

Once you are successfully connected, the button should now say **Disconnect**, and you should see a green <mark style="color:green;">**Connection success**</mark> message.
