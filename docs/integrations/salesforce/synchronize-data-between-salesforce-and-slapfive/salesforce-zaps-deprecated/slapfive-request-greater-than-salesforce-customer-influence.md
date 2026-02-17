---
description: >-
  Anytime a Request is submitted from a Salesforce Opportunity and is then
  updated in SlapFive, update the SlapFive Customer Influence object in
  Salesforce.
---

# SlapFive Request > Salesforce Customer Influence

{% hint style="info" %}
While setting up this Zap, it needs to retrieve a recently changed Request record from your SlapFive instance so that you can map its fields and test your configuration. Before starting, submit a new Request from a Salesforce Opportunity.
{% endhint %}

While logged into your Zapier account, [click here](https://zapier.com/shared/942aad17b9efa30391a6f3c9a4d447ff8ad9e233) to go to the share page for this Zap, and click the **Try this Zap** button.

### 1. Trigger to listen for a new or changed Request in SlapFive

1. On the **Choose account** screen, select your **Connected Account** for SlapFive and click **Continue**.
2. Click the **Test trigger** button, and you will see the data for one of your requests, then click **Continue**.

### 2. Action to find the SlapFive Customer Influence Record in Salesforce or Create it

1. On the **Choose app & event** screen, click **Continue**.
2. On the **Choose account** screen, select your **Connected Account** for Salesforce and click **Continue**.
3. On the **Set up action** screen, in the **Salesforce Object** field, search on _SlapFive_ and select **SlapFive Customer Influence.** Make sure the fields are mapped as follows and click **Continue**:
   * [ ] Field to Search By: **SlapFive Request ID**
   * [ ] Search Value: **1. ID: ...**\
     \
     Check **Create Salesforce Record if it doesn't exist yet** to expand the entry screen.
   * [ ] Record Type: **Customer Reference Request**
   * [ ] Opportunity: **1. Opportunity ID: ...**
   * [ ] SlapFive Request: **1. ID: ...**
4. On the **Test action** screen, click **Test & Review** to make sure that a SlapFive Customer Influence record is created in Salesforce.

### 3. Action to Update the SlapFive Customer Influence Record in Salesforce

1. Click to open Step 3.
2. On the **Choose account** screen, select your **Connected Account** for Salesforce and click **Continue**.
3. On the **Set up action** screen, in the **Salesforce Object** field, search on _SlapFive_ and select **SlapFive Customer Influence.** Make sure the fields are mapped as follows and click **Continue**:
   * [ ] Record to Update: **2. ID: ...**
   * [ ] Record Type: **Customer Reference Request**
   * [ ] Activity Type: **1. Activity Type Name: ...**
   * [ ] Assigned To: **1. Assigned To Name: ...**
   * [ ] Date: **1. Request Date: ...**
   * [ ] For This Prospect Or Purpose: **1. Need For: ...**
   * [ ] Fulfillment Date: **1. Fulfillment Date: ...**
   * [ ] Influence Event: **Customer Reference Request**
   * [ ] Need: **1. Need Description: ...**
   * [ ] Need By Date: **1. Need By Date: ...**
   * [ ] Note To Requester: **1. Note To Requester: ...**
   * [ ] Preferred Customers: **1. Preferred Customers: ...**
   * [ ] Rating Description: **1. Rating Description: ...**
   * [ ] Request Notes: **1. Note: ...**
   * [ ] Request Number: **1. Number: ...**
   * [ ] Request Status: **1. Request Status: ...**
   * [ ] Requester Rating: **1. Rating: ...**
   * [ ] Requester: **1. Requester External ID: ...**
   * [ ] SlapFive Request: **1. ID: ...**
   * [ ] Team: **1. Team Name: ...**
4. On the **Test action** screen, click **Test & Review** to make sure that the SlapFive Customer Influence record is updated in Salesforce.
5. If the test is successful, click the **Turn on Zap** button, otherwise check your field mappings.
