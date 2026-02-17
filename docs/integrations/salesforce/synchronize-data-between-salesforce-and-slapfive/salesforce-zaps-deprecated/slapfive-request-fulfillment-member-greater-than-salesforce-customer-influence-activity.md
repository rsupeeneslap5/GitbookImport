---
description: >-
  When a Fulfillment Member for a Request that was submitted from a Salesforce
  Opportunity is created or updated, update the SlapFive Customer Influence
  Activity object in Salesforce.
---

# SlapFive Request Fulfillment Member > Salesforce Customer Influence Activity

{% hint style="info" %}
While setting up this Zap, it needs to retrieve a recently changed Request Fulfillment Member record from your SlapFive instance so that you can map its fields and test your configuration. Before starting, add a Fulfillment Member to the Request you created for mapping the prior Zap.
{% endhint %}

While logged into your Zapier account, [click here](https://zapier.com/shared/7a25661728422f30a10fe05a890650ef5302d1c6) to go to the share page for this Zap, and click the **Try this Zap** button.

### 1. Trigger to listen for a new or changed Request Fulfillment Member in SlapFive

1. On the **Choose account** screen, select your **Connected Account** for SlapFive and click **Continue**.
2. Click the **Test trigger** button, and you will see a Request Fulfillment Member for one of your Requests, then click **Continue**.

### 2. Action to Assign Influence Score to Completed Activities

This step lets you assign what Influence Score you want to assign when a customer performs a reference activity. You can assign one score for all requests, or you can give different scores based on Activity Type.

1. On the **Choose app & event** screen, click **Continue**.
2. On the **Set up action** screen, in the **Formula** field, change the number _40_ to whatever Influence Score you want to assign and click **Continue**.
3. On the **Test action** screen, click **Test & Review** and confirm that the _output_ field shows the correct score for your sample data.

### 3. Action to find the SlapFive Customer Influence Record in Salesforce

1. On the **Choose app & event** screen, click **Continue**.
2. On the **Choose account** screen, select your **Connected Account** for Salesforce and click **Continue**.
3. On the **Set up action** screen, in the **Salesforce Object** field, search on _SlapFive_ and select **SlapFive Customer Influence.** Make sure the fields are mapped as follows and click **Continue**:
   * [ ] Field to Search By: **SlapFive Request ID**
   * [ ] Search Value: **1. Request ID: ...**
4. On the **Test action** screen, click **Test & Review** and confirm that Zapier found the record.

### 4. Action Find Contact Record in Salesforce to get Contact ID and Account ID

1. Click to open Step 4.
2. On the **Choose app & event** screen, click **Continue**.
3. On the **Choose account** screen, select your **Connected Account** for Salesforce and click **Continue**.
4. On the **Set up action** screen, in the **Salesforce Object** field, search on _Contact_ and select **Contact.** Make sure the fields are mapped as follows and click **Continue**:
   * [ ] Field to Search By: **Email**
   * [ ] Search Value: **1. Email: ...**
5. On the **Test action** screen, click **Test & Review** and confirm that Zapier found the record.

### 5. Action to find the SlapFive Customer Influence Activity Record in Salesforce or Create it

1. Click to open Step 5.
2. On the **Choose app & event** screen, click **Continue**.
3. On the **Choose account** screen, select your **Connected Account** for Salesforce and click **Continue**.
4. On the **Set up action** screen, in the **Salesforce Object** field, search on _SlapFive_ and select **SlapFive Customer Influence Activity.** Make sure the fields are mapped as follows and click **Continue**:
   * [ ] Field to Search By: **SlapFive FulfillmentId**
   * [ ] Search Value: **1. ID: ...**
   * [ ] Record Type: **Customer Reference Activity Performed**
   * [ ] SlapFive Customer Influence: **3. ID: ...**&#x20;
   * [ ] SlapFive FulfillmentId: **1. ID: ...**&#x20;
5. On the **Test action** screen, click **Test & Review** to make sure that a SlapFive Customer Influence record is created in Salesforce.

### 6. Action to Update the SlapFive Customer Influence Activity Record in Salesforce

1. Click to open Step 6.
2. On the **Choose app & event** screen, click **Continue**.
3. On the **Choose account** screen, select your **Connected Account** for Salesforce and click **Continue**.
4. On the **Set up action** screen, in the **Salesforce Object** field, search on _SlapFive_ and select **SlapFive Customer Influence Activity.** Make sure the fields are mapped as follows and click **Continue**:
   * [ ] Record to Update: **5. ID: ...**
   * [ ] Record Type: **Customer Reference Activity Performed**
   * [ ] Fulfilled By Company: **4. Account ID: ...**
   * [ ] Fulfilled By Customer: **4. ID: ...**
   * [ ] Fulfillment Status: **1. Fulfillment Member Status: ...**
   * [ ] Influence Activity: **Customer Reference Activity Performed**
   * [ ] Opportunity: **3. Opportunity C: ...**
   * [ ] Activity Date: **1. Status Change Date: ...**
   * [ ] SlapFive FulfillmentId: **1. ID: ...**
   * [ ] Influence Score: **2. Output: ...**
   * [ ] Activity Type: **1. Activity Type Name: ...**
   * [ ] SlapFive RequestId: **1. RequestId: ...**
5. On the **Test action** screen, click **Test & Review** to make sure that the SlapFive Customer Influence Activity record is updated in Salesforce.
6. If the test is successful, click the **Turn on Zap** button, otherwise check your field mappings.
