---
description: >-
  This section describes how to activate SlapFive's native Revenue Influence
  tracking and reporting capabilities.
---

# Revenue Influence

### Set up Revenue Influence in Client Settings

1. Go to **Admin > Client Settings > Revenue Influence** tab.
2. In the **Influence Activity Type Scoring** section, modify the **Default Score** for each Influence Activity if you want a different score for what is already there, and click **Save**. Focus on:&#x20;
   1. **Fulfillment** - the score assigned when Request Fulfillment Members are Completed.
   2. **View** - the score assigned when Stories or Boards are shared and viewed.
   3. **Referral Activity** - the score assigned when a customer submits a referral.
3. In the **Refresh Influence Events** section, click the **Refresh** button. This creates SlapFive Revenue Influence Event and Influence Activity records for all Requests and Shares/Views that already exist in SlapFive with Opportunity IDs attached.
4. In the **Backfill Missing Opportunities** section, click the **Create Missing Opportunities** button. This creates full SlapFive Opportunity records for every Opportunity ID entered on a Request.

### Copy Revenue Influence Dashboard to Client Instance

This is performed by your SlapFive CSM.

1. Go to **Admin > Manage Clients > Clients** tab.
2. Scroll down to the client instance, and click the blue **Copy Sandbox Dashboards** button.
3. Go to **Dashboards**, and verify that the Revenue Influence dashboard tab appears.

### Activate the Refresh Opportunities automation

This is performed by SlapFive. In the SlapFive Automation Server, activate the automation that refreshes SlapFive Opportunity data from the corresponding records in the CRM.
