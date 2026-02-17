---
description: >-
  This section covers how to establish your Gradual Connection within SlapFive's
  Embedded Integration.
---

# Connect to Gradual

To protect the security and privacy of your Gradual data, SlapFive's Embedded Integration eliminates the need for you to email or message us with your Gradual authentication credentials. You or your Gradual Admin can simply connect right from within SlapFive. You only have to do this once and it will be used for all Gradual data synchronization scenarios. The login data is encrypted and stored within the Embedded Integration.

Before starting this Connection process, you must email support@gradual.com and request your Gradual Authorization Key and x-client-id Key.

1\. In SlapFive, go to the Admin menu, click **Settings**, and click on the **Integrations** sub-tab.

2\. Click the **Gradual Connection** box to expand it. Enter the following fields and click **Connect**.

* [ ] **Connection type:** Leave this set to **Cloud**.
* [ ] **Authentication type:** Select **Header auth**.
* [ ] Under **Header authorization:** Click the **Show** box to expand it and click the **Add Headers** button.
* [ ] You'll see the first pair of entry fields for **Key** and **Value**.
  * [ ] **Key:** Where it says Enter key, type _Authorization_.
  * [ ] **Value:** In the Value field, type _Bearer_, space, then paste your Gradual **token** (which is also the Client Secret in Gradual's API doc). &#x20;
* [ ] Click the **+Add headers** button and you'll see the second pair of entry fields for **Key** and **Value**.
  * [ ] **Key:** Where it says Enter key, type _x-client-id_.
  * [ ] **Value:** Paste your Gradual **clientId**.
* [ ] **Base URL:** Leave this field blank.
* [ ] **Use custom TLS/SSL certificate settings:** Leave this set to No.

Once you are successfully connected, the button should now say **Disconnect**, and you should see a green <mark style="color:green;">**Connection success**</mark> message.
