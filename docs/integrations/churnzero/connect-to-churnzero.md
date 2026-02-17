---
description: >-
  This section covers how to establish your ChurnZero Connection within
  SlapFive's Embedded Integration.
---

# Connect to ChurnZero

To protect the security and privacy of your ChurnZero data, SlapFive's Embedded Integration eliminates the need for you to email or message us with your API Key. You or your ChurnZero Admin can simply connect to ChurnZero right from within SlapFive. You only have to do this once and it will be used for all data synchronization and autoomation scenarios. The login data is then encrypted and stored within the Embedded Integration.

1\. In SlapFive, go into **Settings**, and click on the **Integrations** sub-tab.

2\. Click the **ChurnZero Connection** box to expand it. Enter the following fields and click **Connect**.

* [ ] **Connection type:** Leave this set to **Cloud**.
* [ ] **Authentication type:** Select **Header auth**.
* [ ] Under **Header authorization:** Click the **Show** box to expand it and click the **Add Headers** button.
* [ ] You'll see a pair of entry fields for **Key** and **Value**.
  * [ ] **Key:** Type _Authorization_.
  * [ ] **Value:** Type _AppKey_, then hit space, then paste your ChurnZero API Key.  To generate a new API Key in ChurnZero, go to **Admin > Application Keys**, click the **New App Key** button, give it a name, copy it, and save it.
* [ ] **Base URL:** Leave this field blank.
* [ ] **Use custom TLS/SSL certificate settings:** Leave this set to No.

Once you are successfully connected, the button should now say **Disconnect**, and you should see a green <mark style="color:green;">**Connection success**</mark> message.
