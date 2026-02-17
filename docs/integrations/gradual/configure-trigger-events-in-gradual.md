---
description: >-
  This section covers how to set up a Webhook in Gradual for triggering
  automation workflows.
---

# Configure Trigger Events in Gradual

With SlapFive, you can create automated worfklows that are triggered from events that happen in your Gradual community. Here are some examples:

<table><thead><tr><th width="498">Example Workflow</th><th>Trigger</th></tr></thead><tbody><tr><td>When a new Gradual user is added, create or update their Member record in SlapFive.</td><td>New User is Created</td></tr><tr><td>When a new Gradual user registers and completes their profile, add/update their Member record in SlapFive with the responses they gave to the profile questions.</td><td>User Completes Onboarding</td></tr><tr><td>When a Gradual user attends an event, add an Activity record for their Member record in SlapFive.</td><td>User Attends an Event</td></tr><tr><td>When a Gradual user joins a club that represents a cohort like a user group or CAB, update their Member record in SlapFive.</td><td>User Joined a Club</td></tr></tbody></table>

### Design your workflow

1. Work with your SlapFive Coach to define the trigger and the actions in your desired workflow, as well as the data that should be provided at each step.
2. Your SlapFive Coach will begin to define the workflow in SlapFive and provide you with the Webhook Address.

### Configure your Webhook in Gradual

1. In your Gradual Community Dashboard, go to **Integrations**, and locate the **Outbound Webhooks** box.&#x20;
   1. If this is the first time you've used Outbound Webhooks, click the green **Setup** button in the lower left corner of the box.
   2. If you've set up an Outbound Webhook before, click the **...** menu in the lower right corner of that box, select **Configure**. and then click the **+ Add a Webhook** button.
2. Fill out these fields, and click **Submit**.
   * [ ] **Trigger:** Select the desired Trigger event from the dropdown.
   * [ ] **URL:** Paste the Webhook Address provided to you by your SlapFive Coach.
