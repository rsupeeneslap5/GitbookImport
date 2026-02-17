---
description: >-
  This section covers how to establish your Salesforce Connection within
  SlapFive's Embedded Integration.
---

# Connect to Salesforce

### How to connect

In SlapFive, go into **Settings**, and click on the **Integrations** sub-tab.

* [ ] Click the **Salesforce Connection** box to expand it, and click the **Connect** button.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-01-15 144702.png" alt=""><figcaption><p>Salesforce Connection screen in SlapFive Settings</p></figcaption></figure>

* [ ] You will see your **Salesforce Login** window. Enter the login credentials for your integration user and click **Log In**.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-01-15 145119.png" alt=""><figcaption><p>Salesforce Login window</p></figcaption></figure>

You will then be returned to the Salesforce Connection box in SlapFive, and the button should now say **Disconnect**, and you should see a green <mark style="color:green;">**Connection success**</mark> message.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-01-15 152451.png" alt=""><figcaption><p>Connection success message</p></figcaption></figure>

### How it works using the Workato Connected App

When you connect Salesforce from the SlapFive embedded integration server, which embeds **Workato**, Workato initiates an OAuth authorization flow that relies on a Salesforce **Connected App** for Workato.

In most Salesforce orgs, this process is automatic. In some orgs—typically those with stricter security controls—Salesforce does **not** complete all required steps deterministically.

Here's what it does:

* The first connection attempt **creates or surfaces** the _Workato Connected App_ in Salesforce Setup
* Depending on org security settings, Salesforce may:
  * Automatically install and allow the app, **or**
  * Leave the app present but **not installed or blocked**
* If the app is not fully installed and unblocked, the OAuth flow fails and the connection does not complete

#### What to do if the Salesforce connection fails

If you see any error while connecting Salesforce from Workato:

1. In Salesforce, go to **Setup → Connected Apps → Manage Connected Apps.**
2. Locate and click **Workato.**
3. Verify the following:
   * If **Install** is available, click **Install**
   * If **Unblock** is available, click **Unblock**
4. Return to the **SlapFive Client Settings > Integrations** tab and retry the Salesforce connection

Once the app is both **installed** and **unblocked**, the connection should succeed.
