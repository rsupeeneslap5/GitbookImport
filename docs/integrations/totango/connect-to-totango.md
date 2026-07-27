---
description: >-
  This section covers how to establish your Totango Connection within SlapFive's
  Embedded Integration.
---

# Connect to Totango

To protect the security and privacy of your Totango data, SlapFive's Embedded Integration eliminates the need for you to email or message us with your authentication credentials. You can simply connect right from within SlapFive. You only have to do this once and it will be used for all data synchronization scenarios. The login data is encrypted and stored within the Embedded Integration.

1\. In SlapFive, go to the Admin menu, click **Settings**, and click on the **Integrations** sub-tab.

2\. Click the **Totango Connection** box to expand it. Enter the following fields and click **Connect**.

* [ ] **Connection type:** Leave this set to **Cloud**.
* [ ] **Authentication type:** Select **Header auth** if not already selected.
* [ ] Under **Header authorization:** Click the **Show** box to expand it and click the **Add Headers** button.
* [ ] You'll see the first pair of entry fields for **Key** and **Value**.
  * [ ] **Key:** Where it says Enter key, type _app-token_ if that is not already specified.
  * [ ] **Value:** In the Value field, paste your Totango **API Key/Token**. &#x20;
* [ ] **Base URL:** Leave this field blank.
* [ ] **Use custom TLS/SSL certificate settings:** Leave this set to No.

Once you are successfully connected, the button should now say **Disconnect**, and you should see a green <mark style="color:green;">**Connection success**</mark> message.
