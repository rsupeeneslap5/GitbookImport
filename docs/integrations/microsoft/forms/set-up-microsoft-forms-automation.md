---
description: >-
  This section covers how to set up automation so that a Microsoft Forms
  submission triggers a SlapFive workflow.
---

# Set up Microsoft Forms automation

### **How it works:**

1. A user submits a Microsoft Form.
2. Power Automate captures the submission.
3. Power Automate sends the data to the SlapFive integration server via webhook.
4. The SlapFive automation is triggered to process the data.

### Prerequisites

* Microsoft Form is already created.
* Access to Power Automate with permission to create flows.

### Step 1: Create the Flow in Power Automate

1. Go to Power Automate
2. In the left sidebar, click **Create** and select **Automated cloud flow**
3. In the popup:
   * **Flow name:** `Send Forms to Workato`
   * **Trigger:**  Microsoft Forms → When a new response is submitted
4. Click **Create**

👉 You are now inside the Flow Editor screen\
👉 Everything that follows happens HERE

***

### Step 2: Add “Get Response Details”

You should now see your trigger block. Find this trigger:

```
[When a new response is submitted]
```

1. Below the trigger, click **+ New step**
2. In the search box:
   * Type: `Get response details`
3. Select: **Microsoft Forms → Get response details**
4. Configure it like this:

* [ ] **Form ID:** Select the same form as Step 2
* [ ] **Response ID:** Click into the field, and on the right panel (Dynamic content), select:\
  **Response Id**

👉 At this point your flow should look like:

```
[Trigger] When a new response is submitted
        ↓
[Action] Get response details
```

### Step 3: Add HTTP Action to Send to SlapFive

1. Click **+ New step**
2.  Search:

    ```
    HTTP
    ```
3. Select: **HTTP (Premium)**
4. Configure the HTTP action as follows:

* [ ] **Method:**  POST
* [ ] **URI:** Paste the webhook URL provided by your SlapFive coach.
* [ ] **Headers:** Click **+ Add new parameter → Headers**

Add:

```
Content-Type : application/json
x_webhook_secret : your_shared_secret   (optional)
```

* [ ] **Body:** Click into the Body field → use Dynamic Content panel. Map each field using dynamic content from “Get response details”

Example:

```
{
  "form_name": "Customer Intake Form",
  "submitted_at": "@{utcNow()}",
  "response_id": "@{triggerOutputs()?['body/responseId']}",
  "responder_email": "@{outputs('Get_response_details')?['body/responder']}",
  "answers": {
    "first_name": "@{outputs('Get_response_details')?['body/FirstName']}",
    "last_name": "@{outputs('Get_response_details')?['body/LastName']}",
    "company": "@{outputs('Get_response_details')?['body/Company']}",
    "use_case": "@{outputs('Get_response_details')?['body/UseCase']}"
  }
}
```

### Step 4: Test the automationIntegration

1. Submit a test response in Microsoft Forms
2. Check: Power Automate flow run history → should succeed
