---
description: >-
  This section covers how to trigger an automated workflow based on changes to
  customer health scores or other data in Gainsight, rather than user actions.
---

# Trigger an automated workflow from Gainsight health score changes

This rule runs on a schedule (e.g., every 15 minutes or hourly). When the defined conditions are met, Gainsight will send a POST request to the webhook URL, triggering the downstream workflow.

### Set up a Rule

Go to **Administration > Rules Engine > Rules List** and create a new Rule.

**Dataset**

Click **DATASET** to configure the data source.

* **Source Object:** Select **Scorecard Fact**
* Configure filters such as:
  * Score is modified
  * Score meets threshold conditions (e.g., drops below 70)

> Note: Account Scorecard History is a system snapshot object and is not typically used directly for triggering events. Scorecard Fact should be used for detecting changes.

### Add Action: Call External API

On the **Actions** tab, select **Call External API**.

* **Method:** POST
* **URL:** Paste the webhook URL provided by your SlapFive CSM.
* **Payload Type:** Plain (JSON)

**Sample Payload**

```
{
  "companyName": "{{Company Name}}",
  "companyId": "{{Company ID}}",
  "score": "{{Score}}",
  "previousScore": "{{Previous Score}}",
  "modifiedDate": "{{Modified Date}}"
}
```

#### Field Mapping

Map fields from the dataset to the JSON payload.

Include:

* Company identifiers
* Score values
* Timestamps
* Any additional context needed downstream
