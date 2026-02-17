---
description: >-
  When a SlapFive Activity is created or updated, create or update a SlapFive
  Customer Activity record in Salesforce.
---

# SlapFive Activity > Salesforce Customer Activity

{% hint style="info" %}
While setting up this Zap, it needs to retrieve a recent Activity record from your SlapFive instance so that you can map its fields and test your configuration. Before starting, make sure you  have at least one Activity record.
{% endhint %}

While logged into your Zapier account, [click here](https://zapier.com/shared/1d27c857838c6f5a4b4b940487fb0d8bb357db6b) to go to the share page for this Zap, and click the **Try this Zap** button.

### 1. Trigger to listen for a new or changed Activity in SlapFive

1. On the **Choose account** screen, select your **Connected Account** for SlapFive and click **Continue**.
2. Click the **Test trigger** button, and you will see the data for one of your requests, then click **Continue**.

### 2. Action to find the Contact Record in Salesforce for Member who performed the Activity

1. On the **Choose app & event** screen, click **Continue**.
2. On the **Choose account** screen, select your **Connected Account** for Salesforce and click **Continue**.
3. On the **Set up action** screen, in the **Salesforce Object** field, search on _SlapFive_ and select **Contact.** Make sure the fields are mapped as follows and click **Continue**:
   * [ ] Field to Search By: **Email**
   * [ ] Search Value: **1. Customer Email: ...**
4. On the **Test action** screen, click **Test & Review** to make sure that the Contact record for this customer was found in Salesforce.

### 3. Action to see if this SlapFive Activity Record already exists in Salesforce

1. Click to open Step 3.
2. On the **Choose account** screen, select your **Connected Account** for Salesforce and click **Continue**.
3. On the **Set up action** screen, in the **Salesforce Object** field, search on _SlapFive_ and select **SlapFive Customer Activity.** Make sure the fields are mapped as follows and click **Continue.**
   * [ ] Field to Search By: **SlapFive Activity ID**
   * [ ] Search Value: **1. ID: ...**
   * [ ] SlapFive Activity: **1. ID: ...**
4. On the **Test action** screen, click **Test & Review** and make sure that the SlapFive Activity record was found or created in Salesforce.

### 4. Action to Update the SlapFive Customer Influence Record in Salesforce

1. Click to open Step 4.
2. On the **Choose account** screen, select your **Connected Account** for Salesforce and click **Continue**.
3. On the **Set up action** screen, in the **Salesforce Object** field, search on _SlapFive_ and select **SlapFive Customer Activity.** Make sure the fields are mapped as follows and click **Continue.** If you get a box that says **Extra Fields**, DO NOT click the **Remove these extra fields** button.
   * [ ] Record to Update: **3. ID: ...**
   * [ ] Activity Type: **1. Activity Type Name: ...**
   * [ ] Account: **2. Account ID: ...**
   * [ ] Activity Date: **1. Date Time: ...**
   * [ ] Contact: **2. ID: ...**
   * [ ] Engagement Score: **1. Activity Type Points: ...**
   * [ ] Notes: **1. Notes: ...**
   * [ ] Related To Opportunity: **1. Opportunity ID: ...**
   * [ ] Responded To This Prompt: **1. Prompt Title: ...**
   * [ ] SlapFive Activity: **1. ID: ...**
   * [ ] Viewed This Board: **1. Board Name: ...**
   * [ ] Prompt Response Story URL: **1. Story URL: ...**
4. On the **Test action** screen, click **Test & Review** to make sure that the SlapFive Customer Influence record is updated in Salesforce.
5. If the test is successful, click the **Turn on Zap** button, otherwise check your field mappings.
