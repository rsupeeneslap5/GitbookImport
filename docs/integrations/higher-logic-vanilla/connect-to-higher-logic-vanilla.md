---
description: >-
  This section covers how to establish your Higher Logic Vanilla Connection
  within SlapFive's Embedded Integration.
---

# Connect to Higher Logic Vanilla

To protect the security and privacy of your Vanilla data, SlapFive's Embedded Integration eliminates the need for you to email or message us with your Vanilla authentication credentials. You or your Vanilla Admin can simply connect to Vanilla right from within SlapFive. You only have to do this once and it will be used for all Vanilla data synchronization scenarios. The login data is encrypted and stored within the Embedded Integration.

1\. In SlapFive, go to the Admin menu, click **Settings**, and click on the **Integrations** sub-tab.

2\. Click the **Higher Logic Vanilla Connection** box to expand it. Enter the following fields and click **Connect**.

* [ ] **Connection type:** Leave this set to **Cloud**.
* [ ] **Authentication type:** Select **Header auth**.
* [ ] **Header authorization:** Click the **Show** box to expand it and click the **Add Headers** button.
* [ ] **Key:** Where it says Enter key, type _Authorization_.
* [ ] **Value:** Type the word _Bearer_, followed by a space, then paste your **Access Token**. See the [Authenticating APIv2 calls with Personal Access Tokens](https://success.vanillaforums.com/kb/articles/41-authenticating-apiv2-calls-with-personal-access-tokens) page in the Vanilla documentation for instructions on how to generate your Access Token.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-13 132251 (1).png" alt=""><figcaption><p>Higher Logic Vanilla Connection Screen</p></figcaption></figure>

* [ ] **Base URL:** Leave this field blank.
* [ ] **Use custom TLS/SSL certificate settings:** Leave this set to No.

Once you are successfully connected, the button should now say **Disconnect**, and you should see a green <mark style="color:green;">**Connection success**</mark> message.
