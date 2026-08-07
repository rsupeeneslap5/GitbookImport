---
description: >-
  This section covers how to configure Planhat to send a webhook notification
  whenever a Company's Health Score changes, so it can be picked up by the
  SlapFive integration.
---

# Send Planhat health score changes to SlapFive

#### 1. Open the Automations Apps Library

In Planhat, navigate to **Automations** and open the **Apps Library**.

#### 2. Find the Health Score webhook template

Use the search box in the top right of the Apps Library and type `webhook` to filter results, then locate:

**"Notify a webhook when a Company's Health Score changes"**

This is one of roughly 20 prebuilt "Notify a webhook" templates in the library — make sure you select the Health Score variant specifically, not a similarly named one (e.g. NPS change, Phase change).

#### 3. Configure the template

Click into the template and set:

* **Company filter** _(optional)_ — scope this to a specific segment or set of Companies if you don't want every Company's Health Score change to trigger a notification. Leave blank to apply to all Companies.
* **Webhook URL** — paste in the Webhook URL provided by your SlapFive CSM.
* **Payload format** — select **JSON**.
* **Custom message** — the template pre-populates a message using dynamic replacement codes (e.g. references to the Company name, old/new score). This can be left as-is or customized; it does not need to be edited for the integration to function correctly, but review it to confirm it includes the fields the integration needs.

#### 4. Save and activate

Save the Automation and make sure it's enabled/turned on in the App Center. A Templated Automation configured but left disabled will not fire.

#### 5. Test the notification

Trigger a Health Score change on a test Company record (or use whatever test mechanism is available in the template) to confirm data is flowing.

To verify the webhook fired correctly:

1. Open the Automation's **logs**.
2. Click into the **Event details** for the most recent run.
3. Confirm the payload was sent successfully (look for a successful delivery status, not an error/retry state).

#### 6. Share confirmation with your integration contact

Once you've confirmed a test event fired successfully, let your SlapFive CSM know so they can confirm receipt by the SlapFive integration server and finish configuring the SlapFive sync.
