---
description: >-
  When a Fulfillment Board for a Request that was submitted from a Salesforce
  Opportunity is created or updated, update the SlapFive Customer Influence
  Activity object in Salesforce.
---

# SlapFive Request Fulfillment Board > Salesforce Customer Influence Activity

{% hint style="info" %}
While setting up this Zap, it needs to retrieve a recently changed Request Fulfillment Board from your SlapFive instance so that you can map its fields and test your configuration. Before starting, add a Fulfillment Board to the Request you created for mapping the prior Zap.
{% endhint %}

While logged into your Zapier account, [click here](https://zapier.com/shared/8b92a67b288327bff4bb8018e555eb8308e855a3) to go to the share page for this Zap, and click the **Try this Zap** button.

### 1. Trigger to listen for a new or changed Request Fulfillment Board in SlapFive

1. On the **Choose account** screen, select your **Connected Account** for SlapFive and click **Continue**.
2. Click the **Test trigger** button, and you will see a Request Fulfillment Member for one of your Requests, then click **Continue**.

### 2. Action to find the SlapFive Customer Influence Record in Salesforce

1. On the **Choose app & event** screen, make sure **Salesforce** is selected and click **Continue**.
2. On the **Choose account** screen, select your **Connected Account** for Salesforce and click **Continue**.
3. On the **Set up action** screen, in the **Salesforce Object** field, search on _SlapFive_ and select **SlapFive Customer Influence.** Make sure the fields are mapped as follows and click **Continue**:
   * [ ] Field to Search By: **SlapFive Request ID**
   * [ ] Search Value: **1. Request ID: ...**
4. On the **Test action** screen, click **Test & Review** and confirm that Zapier found the record.

### 3. Action to find the SlapFive Customer Influence Activity Record in Salesforce or Create it

1. Click to open Step 3.
2. On the **Choose app & event** screen, make sure **Salesforce** is selected and click **Continue**.
3. On the **Choose account** screen, select your **Connected Account** for Salesforce and click **Continue**.
4. On the **Set up action** screen, in the **Salesforce Object** field, search on _SlapFive_ and select **SlapFive Customer Influence Activity.** Make sure the fields are mapped as follows and click **Continue**:
   * [ ] Field to Search By: **SlapFive FulfillmentId**
   * [ ] Search Value: **1. ID: ...**
   * [ ] Record Type: **Customer Reference Activity Performed**
   * [ ] SlapFive Customer Influence: **2. ID: ...**&#x20;
   * [ ] SlapFive FulfillmentId: **1. ID: ...**&#x20;
5. On the **Test action** screen, click **Test & Review** to make sure that a SlapFive Customer Influence record is created in Salesforce.

### 4. Action to Update the SlapFive Customer Influence Activity Record in Salesforce

1. Click to open Step 4.
2. On the **Choose app & event** screen, make sure **Salesforce** is selected and click **Continue**.
3. On the **Choose account** screen, select your **Connected Account** for Salesforce and click **Continue**.
4. On the **Set up action** screen, in the **Salesforce Object** field, search on _SlapFive_ and select **SlapFive Customer Influence Activity.** Make sure the fields are mapped as follows and click **Continue**:
   * [ ] Record to Update: **3. ID: ...**
   * [ ] Record Type: **Customer Reference Activity Performed**
   * [ ] Fulfillment Status: _**Sent**_
   * [ ] Activity Date: **1. Status Change Date: ...**
   * [ ] Influence Activity: **Customer Reference Content Sent**
   * [ ] Opportunity: **2. Opportunity C: ...**
   * [ ] Activity Date: **1. Created At: ...**
   * [ ] Fulfilled By SlapFive Content URL: **1. Board URL: ...**
   * [ ] Fulfilled By SlapFive Content: **1. Board ID: ...**
   * [ ] Fulfilled By SlapFive Content Name: **1. Board Name: ...**
   * [ ] SlapFive FulfillmentId: **1. ID: ...**
   * [ ] Influence Score: **Enter the score you want to give to this event**
   * [ ] SlapFive RequestId: **1. RequestId: ...**
5. On the **Test action** screen, click **Test & Review** to make sure that the SlapFive Customer Influence Activity record is updated in Salesforce.
6. If the test is successful, click the **Turn on Zap** button, otherwise check your field mappings.
