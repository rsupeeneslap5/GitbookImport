---
description: >-
  This section covers how to establish your Gainsight CC Connection within
  SlapFive's Embedded Integration.
---

# Connect to Gainsight CC (Insided)

To protect the security and privacy of your Gainsight CC data, SlapFive's Embedded Integration eliminates the need for you to email or message us with your authentication credentials. You or your Gainsight Community Admin can simply connect to Gainsight CC right from within SlapFive. You only have to do this once and it will be used for all data synchronization scenarios. The login data is encrypted and stored within the Embedded Integration.

1\. In Gainsight CC, go to **Integrations** > **API**. In the **OAuth2** section, click the **Create an OAuth2 client**, and keep this screen open.

<figure><img src="../../.gitbook/assets/Screenshot 2024-06-01 130854.png" alt=""><figcaption><p>Gainsight CC API page</p></figcaption></figure>

2\. In SlapFive, go to the Admin menu, click **Settings**, and click on the **Integrations** sub-tab.&#x20;

3\. Click the **Gainsight CC Connection** box to expand it. Enter the following fields and click **Connect**.

* [ ] **Connection type:** Leave this set to **Cloud**.
* [ ] **Authentication type:** Select **OAuth 2 (client credentials grant)** if not already selected.
* [ ] **OAuth2 token URL:** Copy the **Your API base URL** from the Gainsight CC API page and paste it here, the append it with _/oauth2/token_.
* [ ] **OAuth2 client ID:** Copy the **Client ID** from the Gainsight CC **OAuth2 client** box you opened in Step 1 and paste it here.
* [ ] **OAuth2 client secret:** Copy the **Client secret** from the Gainsight CC **OAuth2 client** box you opend in Step 1 and paste it here.
* [ ] &#x20;**How does the API require credentials to be sent to request a token?**: Select **Header**.
* [ ] **Base URL:** Copy the **Your API base URL** from the Gainsight CC API page and paste it here.
* [ ] **Use custom TLS/SSL certificate settings:** Leave this set to No.

<figure><img src="../../.gitbook/assets/Screenshot 2024-06-01 131501.png" alt=""><figcaption><p>Gainsight CC Connection screen</p></figcaption></figure>

Once you are successfully connected, the button should now say **Disconnect**, and you should see a green <mark style="color:green;">**Connection success**</mark> message.
