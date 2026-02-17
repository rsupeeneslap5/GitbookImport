---
description: >-
  When a SlapFive content asset that was shared from a Salesforce Opportunity is
  then viewed by the recipient, write a SlapFive Customer Influence Activity
  record in Salesforce.
---

# SlapFive Content View > Salesforce Customer Influence Activity

{% hint style="info" %}
While setting up this Zap, it needs to retrieve a recent Content View record from your SlapFive instance so that you can map its fields and test your configuration. Before starting, view the board you shared from a Salesforce Opportunity in the previous Zap.
{% endhint %}

While logged into your Zapier account, [click here](https://zapier.com/shared/f4e0472f6bca85a4a9986f4280e0a85ecc8b4ca8) to go to the share page for this Zap, and click the **Try this Zap** button.

### 1. Trigger to listen for a new Content Share in SlapFive

1. On the **Choose account** screen, select your **Connected Account** for SlapFive and click **Continue**.
2. Click the **Test trigger** button, and you will see the data for one of your Content Views, then click **Continue**.

### 2. Action to find the SlapFive Customer Influence Record in Salesforce or Create it

1. On the **Choose app & event** screen, click **Continue**.
2. On the **Choose account** screen, select your **Connected Account** for Salesforce and click **Continue**.
3. On the **Set up action** screen, in the **Salesforce Object** field, search on _SlapFive_ and select **SlapFive Customer Influence.** Make sure the fields are mapped as follows and click **Continue**:
   * [ ] Field to Search By: **SlapFive Share ID**
   * [ ] Search Value: **1. ID: ...**
4. On the **Test action** screen, click **Test & Review** to make sure that a SlapFive Customer Influence record is created in Salesforce.

### 3. Action to Create the SlapFive Customer Influence Activity Record in Salesforce

1. Click to open Step 3.
2. On the **Choose account** screen, select your **Connected Account** for Salesforce and click **Continue**.
3. On the **Set up action** screen, in the **Salesforce Object** field, search on _SlapFive_ and select **SlapFive Customer Influence Activity.** Make sure the fields are mapped as follows and click **Continue**:
   * [ ] Record Type: **Customer Content Shared and Viewed**
   * [ ] SlapFive Customer Influence: **2. ID: ...**
   * [ ] Influence Activity: **Customer Content Shared and Viewed**
   * [ ] Opportunity: **2. Opportunity C: ...**
   * [ ] Activity Date: **1. Created At: ...**
   * [ ] For This Prospect Or Purpose: **1. Need For: ...**
   * [ ] SlapFive Content View Details Link: _**https://slapfive.slapfive.com/client/tracking/share**_**&#x20;1. Share ID: ...**
   * [ ] Influence Score: Type the number that represents the Influence Score you want to assign to shared content views.
4. On the **Test action** screen, click **Test & Review** to make sure that the SlapFive Customer Influence Activity record is created in Salesforce.
5. If the test is successful, click the **Turn on Zap** button, otherwise check your field mappings.

###
