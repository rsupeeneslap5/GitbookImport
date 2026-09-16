---
description: >-
  This section covers how to establish your connection to SlapFive from Claude
  Cowork.
---

# Connect to SlapFive from Claude Cowork

SlapFive has enabled you to connect to SlapFive's MCP Server from Claude Cowork.

1\. From the Claude Cowork desktop, click on **Customize > Connectors**.

2\. In your list of Connectors, click the **+** button to Add connector, and click **Add custom connector**. Fill in these fields and click the **Continue** button. The values you need for these fields are found in your **SlapFive Client Settings > Integrations** tab.

* [ ] **Name:** Type _SlapFive_.
* [ ] **MCP server URL:** Copy and paste the **MCP SERVER URL** from **Client Settings** > **Integrations** tab.

3. On the Add custom connector screen, do the following and click the **Add** button:

* [ ] **Authentication:** Leave this set to **Sign in now.**
* [ ] **OAuth client:** Click **Use your own OAuth client** and additional fields appear.
* [ ] **OAuth client ID:** Copy and paste the **CLIENT ID** from **Client Settings** > **Integrations** tab.
* [ ] **OAuth client secret (optional):** Copy and paste the **CLIENT SECRET** from **Client Settings** > **Integrations** tab.

4. Click the **Connect** button that appears in the middle of the screen.
5. A new screen appears, click the **Continue connecting** button.
6. You will see the SlapFive login screen. If you are already logged into your SlapFive account, just click your Email address. If you are not already logged in, enter your Username and Password and click the login button.

Once you are successfully connected, you will see SlapFive in the list of connected Connectors. For security purposes, SlapFive connections are set to expire after periods of non-use, so if your login has expired, you will need to repeat steps 3 and 4.

NOTE: When executing Prompts that access SlapFive data, each time Claude Cowork uses a SlapFive AI Skill for the first time, it will ask you for permission. Just click the **Allow for this task** button or click **Enter** to proceed.



{% embed url="https://drive.google.com/file/d/1o_0xzUH6kFVRZP-U0yi2ity0TEzB6Stv/view" %}
