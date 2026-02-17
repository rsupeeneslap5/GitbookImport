---
description: >-
  This section describes how to integrate Eloqua form submissions so they update
  any SlapFive objects.
---

# Eloqua Form Submissions

Here are some example use cases for Eloqua Forms:

* Customers join your advocacy program.
* Customers update their profile and preferences.
* Employees nominate customers.
* Customers refer their friends.

### How to set it up:

1. Your SlapFive CSM will provide you with a Webhook URL that you will use in the next step.
2. In Eloqua, open your Form, and then go to **Processing Steps** → **Add Step** →\
   &#xNAN;**“Post Data to Server (Advanced)”**. Enter the following information and click Save.
   * [ ] **Post URL**: paste the Webhook URL from Step 2
   * [ ] **HTTP Method**: select POST.
3. Provide your CSM with the link to the Eloqua form so we can submit a sample that we'll use to configure the rest of the integration.
