---
description: >-
  This section covers how to establish your TrustRadius Connection within
  SlapFive's Embedded Integration.
---

# Connect to TrustRadius

To protect the security and privacy of your TrustRadius data, SlapFive's Embedded Integration eliminates the need for you to email or message us with your authentication credentials. You or your  Admin can simply connect right from within SlapFive. You only have to do this once and it will be used for all TrustRadius data synchronization scenarios. The login data is encrypted and stored within the Embedded Integration.

1. Contact your TrustRadius CSM or `product@trustradius.com` to obtain your TrustRadius API Key.
2. In SlapFive, go to the **Admin menu**, click **Settings**, and click on the **Integrations** sub-tab.
3. Click the **TrustRadius Connection** box to expand it. Enter the following fields and click **Connect**.
   * [ ] **Connection type:** Leave this set to **Cloud**.
   * [ ] **Authentication type:** Select **Header auth** if not already selected.
   * [ ] Under **Header authorization:** Click the **Show** box to expand it and if you don't see the first pair of entry fields for **Key** and **Value,** click the **Add Headers** button and you'll see them.
     * [ ] **Key:** Where it says Enter key, type _x-api-key_.
     * [ ] **Value:** In the Value field, paste your **TrustRadius API Key** from step 1.
   * [ ] **Base URL:** Leave this field blank.
   * [ ] **Use custom TLS/SSL certificate settings:** Leave this set to No.

Once you are successfully connected, the button should now say **Disconnect**, and you should see a green <mark style="color:green;">**Connection success**</mark> message.
