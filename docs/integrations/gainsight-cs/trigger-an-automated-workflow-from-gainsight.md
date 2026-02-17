---
description: >-
  This section covers how to set up Gainsight to trigger an automated workflow
  from an action a Gainsight user has taken.
---

# Trigger an automated workflow from Gainsight

## Create an External Action

In Gainsight, go to **Administration > External Actions** and click **Create Action**.

* [ ] **Action Name:** Give it a descriptive name that describes the action or event, like _User nominates a customer for SlapFive_.&#x20;
* [ ] **Method:** Select POST
* [ ] **URL:** Paste the Webhook URL provided to you by your SlapFive CSM.
* [ ] **Payload:** Select **Plain**. Then specify the fields in a JSON object format like this. For field names, use the Gainsight field names without spaces. You will almost always need to include the Person's first name, last name, email, and Company name, and should include any other fields that you want captured in SlapFive.

<figure><img src="../../.gitbook/assets/Screenshot 2025-03-20 084855.png" alt=""><figcaption><p>Sample JSON request parameters</p></figcaption></figure>

## Set up a Rule

Go to **Administration > Rules Engine > Rules List** tab and create a new Rule.

* [ ] **Dataset:** Click "DATASET" to configure the data source for the rule.
* [ ] **Task Name:** Enter a descriptive name for the task.
* [ ] **Source Object:** Select the object from which you want to fetch data (e.g., Usage Data, Activity Timeline). Then set the filter conditions you want to apply to narrow down the actions to only include the ones you want to trigger the automation.
* [ ] On the Actions tab, select **Call External API**.
* [ ] **URL:** Paste the same URL that you pasted in the External Action.
* [ ] **Field Mapping:** For each field you included in the Create Action Payload, map the Gainsight field to it.

## Trigger the event

In Gainsight, perform whatever action or event triggers this workflow. This will cause Gainsight to call the webhook URL and pass a payload that the SlapFive CSM can use to configure the rest of the steps in the automation.
