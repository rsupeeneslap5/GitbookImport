---
description: >-
  This section covers how to establish your Seismic Connection within SlapFive's
  Embedded Integration.
---

# Connect to Seismic

To protect the security and privacy of your Seismic data, SlapFive's Embedded Integration eliminates the need for you to email or message us with your authentication credentials. You or your admin can simply connect to Seismic right from within SlapFive. You only have to do this once and it will be used for all integration and automation scenarios. The data is encrypted and stored within the Embedded Integration.

### Create a Seismic App for SlapFive

1. In the Seismic Developers site, go to **My Apps** and click the **Create an app** button. In the **App name** field, enter _SlapFive_ and click the **Create app** button.
2. Click the **Authentication** menu, and in the box that says **Do you need authentication for your app?**, turn it on.
3. In the **Redirect URIs (redirect\_uri)** field, paste this URL _https://www.workato.com/oauth/callback_&#x20;
4. Click the **Save** button at the top.
5. Go back down to the **Client secret (client\_secret)** field and click the **Generate** button.
6. Go down to the **Scopes** section and select all Scopes.
7. Keep this screen open for the next step.

### Connect to Seismic from SlapFive

1. In SlapFive, go to the Admin menu, click **Settings**, and click on the **Integrations** sub-tab.
2. Click the **Seismic Connection** box to expand it. Enter the following fields and click **Connect**.
   * [ ] **Connection type:** Leave this set to **Cloud**.
   * [ ] **Authentication type:** Select **OAuth 2 (authorization code grant)**.
   * [ ] **Endpoint has case-sensitive headers?**: Leave this set to **No**.
   * [ ] **OAuth2 authorization URL:** Paste your authorization URL, which should like like this:\
     &#xNAN;_&#x68;ttps://auth.seismic.com/tenants/\<your\_tenant>/connect/authorize?response\_type=code_
   * [ ] **OAuth2 token URL:** Paste your token URL, which should look like this:\
     &#xNAN;_&#x68;ttps://auth.seismic.com/tenants/\<your\_tenant>/connect/token_
   * [ ] **OAuth2 client ID:** In the SlapFive App you just created in Seismic, copy the **Client id (client\_id)** and paste it here.
   * [ ] **OAuth2 client secret:** In the SlapFive App you just created in Seismic, copy the **Client secret (client\_secret)** and paste it here.
   * [ ] **How does the API require credentials to be sent to request a token?:** Select **Header**.
   * [ ] **Base URL:** Leave this blank.
   * [ ] **Advanced settings:** Click Show
   * [ ] **OAuth2 scopes:** Copy and paste _seismic.library.manage seismic.library.view_.&#x20;
   * [ ] **Token settings:** Select **Use Access Token**.

Once you are successfully connected, the button should now say **Disconnect**, and you should see a green <mark style="color:green;">**Connection success**</mark> message.
