---
description: >-
  This section covers how to establish your G2 Connection within SlapFive's
  Embedded Integration.
---

# Connect to G2

To protect the security and privacy of your G2 data, SlapFive's Embedded Integration eliminates the need for you to email or message us with your authentication credentials. You or your G2 Admin can simply connect right from within SlapFive. You only have to do this once and it will be used for all G2 data synchronization scenarios. The login data is encrypted and stored within the Embedded Integration.

1. In G2, log in to your **G2 Admin account** and go to **Integrations** or **Developer / API Tokens** (exact menu names vary by G2 plan).
   * [ ] Create a new **API Token**
   * [ ] Copy the token value
2. In SlapFive, go to the **Admin menu**, click **Settings**, and click on the **Integrations** sub-tab.
3. Click the **G2 Connection** box to expand it. Enter the following fields and click **Connect**.
   * [ ] **Connection type:** Leave this set to **Cloud**.
   * [ ] **Authentication type:** Select **Header auth** if not already selected.
   * [ ] Under **Header authorization:** Click the **Show** box to expand it and if you don't see the first pair of entry fields for **Key** and **Value,** click the **Add Headers** button and you'll see them.
     * [ ] **Key:** Where it says Enter key, type _Authorization_.
     * [ ] **Value:** In the Value field, type _Bearer_, space, then paste your **G2 API Key** from step 1.
   * [ ] **Base URL:** Leave this field blank.
   * [ ] **Use custom TLS/SSL certificate settings:** Leave this set to No.

Once you are successfully connected, the button should now say **Disconnect**, and you should see a green <mark style="color:green;">**Connection success**</mark> message.
