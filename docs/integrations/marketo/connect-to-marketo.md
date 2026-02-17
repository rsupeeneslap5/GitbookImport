---
description: >-
  This section covers how to establish your Marketo Connection within SlapFive's
  Embedded Integration.
---

# Connect to Marketo

To protect the security and privacy of your Marketo data, SlapFive's Embedded Integration eliminates the need for you to email or message us with your Marketo Client Key or Client Secret. You or your Marketo Admin can simply connect to Marketo right from within SlapFive. You only have to do this once and it will be used for all Marketo integration and data synchronization scenarios. The login data is then encrypted and stored within the Embedded Integration.

1\. In SlapFive, go into **Settings**, and click on the **Integrations** sub-tab.

2\. Click the **Marketo Connection** box to expand it. Enter the following fields and click **Connect**.

* [ ] **REST Endpoint:** Enter the Base URL for accessing the Marketo API. See the [Base URL article](https://developers.marketo.com/rest-api/base-url/) for how to find this URL.
* [ ] **Custom Service client ID:** Create a Custom Service in Marketo and paste your Custom Service client ID. See the [Custom Services article](https://developers.marketo.com/rest-api/custom-services/) for how to access the client ID and client secret.
* [ ] **Custom Service client secret:** Paste your client secet for the Custom Service you created in the prior step.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-20 105124.png" alt=""><figcaption><p>Connect to Marketo</p></figcaption></figure>

Once you are successfully connected, the button should now say **Disconnect**, and you should see a green <mark style="color:green;">**Connection success**</mark> message.
