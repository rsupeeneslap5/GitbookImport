---
description: >-
  This section shows you how to create a Marketo form and send responses to
  SlapFive. Use cases include: advocate nominations, customer referrals,
  approval forms, and onboarding forms.
---

# Send Marketo Form Data to SlapFive

### Process Overview

The automated workflow runs in four steps:

1. **Form:** A prospect fills out a Marketo landing page form with their details.
2. **Smart Campaign:** A Marketo Smart Campaign detects the form submission and triggers automatically.
3. **Webhook:** The campaign calls a configured Webhook that POSTs the form data as JSON to SlapFive's automation server, which updates SlapFive Members, Companies, Campaigns, etc.

### Step 1 — Create the Webhook

The Webhook tells Marketo where to send data and what to include in the request body.

1. In Marketo, navigate to **Admin → Integration → Webhooks**.
2. Click **New Webhook**. The New Webhook dialog opens.
3. Complete each field as follows:

| Field                      | Value to Enter                                                   |
| -------------------------- | ---------------------------------------------------------------- |
| **Webhook Name**           | _Send Form Completion to SlapFive_ (or any descriptive name)     |
| **Description**            | Enter an optional description                                    |
| **URL**                    | Paste the Webhook Trigger URL provided by your SlapFive CSM here |
| **Request Type**           | POST                                                             |
| **Template**               | See JSON body below                                              |
| **Request Token Encoding** | UTF-8                                                            |
| **Response Type**          | JSON                                                             |

**Request Body (Template Field)**

Copy and paste the following JSON, augmented with the rest of your form fields, into the **Template** field. Marketo will automatically replace each token with the lead's field value when the webhook fires.

```json
json

{
  "firstName": "{{lead.First Name}}",
  "lastName":  "{{lead.Last Name}}",
  "email":     "{{lead.Email Address}}",
  "company":   "{{lead.Company Name}}",
  add the rest of the form fields in this format
}
```

**Tokens are case-sensitive.** Use the exact token names from Marketo. You can also click **Insert Token** inside the Template field to browse and pick tokens from a picker rather than typing them manually.

4\. Click **Save**. The webhook now appears in your Webhooks list.

5\.  Reopen the webhook you just saved and click **Add Header**. Add the following header so that SlapFive's server correctly interprets the request body as JSON:

| Header Name  | Header Value     |
| ------------ | ---------------- |
| Content-Type | application/json |

6\. Click **Save** again.

***

### Step 2 — Create the Form

Build the Marketo form that collects the data you want to pass to SlapFive. If you already have a suitable form, skip to Part 3.

1. In Marketo, navigate to **Design Studio → Forms**, or right-click a folder in **Marketing Activities** and choose **New → New Form**.
2. Click **New Form**. Enter a descriptive name (e.g. _Customer Referral Form_) and click **Create**.
3. The Form Editor opens. Add the form fields using the field picker on the left panel:

| Field Label       | Field API Name | Input Type | Required? |
| ----------------- | -------------- | ---------- | --------- |
| **First Name**    | `FirstName`    | Text       | Yes       |
| **Last Name**     | `LastName`     | Text       |           |
| **Email Address** | `Email`        | Email      | Yes       |
| **Company Name**  | `Company`      | Text       |           |

**Mark Email Address as Required.** Marketo uses email address as the unique identifier for lead records. Without a required email field, Marketo cannot create or match leads correctly, which will result in missing data in SlapFive.<br>

4. Click the **Thank You Page** tab and enter a redirect URL or a thank-you message to display after submission.
5. Click **Finish → Approve and Close**. Embed the form on a Marketo Landing Page or copy the **Embed Code** to add it to an external page.

***

### Part 3 — Create the Smart Campaign

The Smart Campaign is the automation engine that listens for form submissions and fires the webhook.

1. In Marketo, go to **Marketing Activities**, right-click the program or folder where this campaign should live and select **New Smart Campaign**. Give it a clear name such as _Webhook — Send to SlapFive_.

**Smart List (Trigger)**

2. Click the **Smart List** tab. From the trigger panel on the right, drag **Fills Out Form** onto the canvas and configure it:

| Setting                   | Value                                           |
| ------------------------- | ----------------------------------------------- |
| **Trigger**               | Fills Out Form                                  |
| **Form**                  | Select the form you created in Part 2           |
| **Web Page** _(optional)_ | Any, or restrict to a specific landing page URL |

**Use a trigger, not a filter.** Using **Fills Out Form** as a trigger means the campaign runs in real time every time the form is submitted. Do not use a filter-only batch approach for webhook calls — the data won't arrive in SlapFive's automation server immediately.<br>

**Flow (Action)**

3. Click the **Flow** tab. Drag **Call Webhook** onto the canvas and configure it:

| Setting     | Value                                     |
| ----------- | ----------------------------------------- |
| **Webhook** | Select the webhook you created in Step 1. |

4. Click the **Schedule** tab. Confirm **Campaign Type** is set to **Triggered**, then click **Activate**. The campaign is now live.

***

### Step 4 — Test the Integration

1. Open the landing page or form preview and submit a test entry with your own name, email address, and company name.
2. In Marketo, go to **Marketing Activities → your Smart Campaign → Results** tab. A **Call Webhook** activity should appear within a few seconds.
3. In SlapFive, check that the records were created or updated. This is typically Member, Company, and Campaign records.
