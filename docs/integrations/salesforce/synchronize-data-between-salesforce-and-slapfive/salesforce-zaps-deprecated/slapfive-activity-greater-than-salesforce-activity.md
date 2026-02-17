---
description: >-
  This Zap creates a Salesforce Activity (Event) records on Contact and Account
  records when a SlapFive Activity record is created.
---

# SlapFive Activity > Salesforce Activity

While logged into your Zapier account, click the **Create Zap** button.

### 1. Trigger to listen for a new or changed Activity in SlapFive:

1. On the **1. Trigger** screen, name your Zap in the upper left, then in the **Search apps…** box, search for **SlapFive**, and select it.
2. In the **Choose an event** box, select **New or Changed Activity** and click **Continue**.
3. On the **Choose account** screen, select your Connected Account for SlapFive and click **Continue**.
4. Click the **Test trigger** button to pull some data into the Zap so you can test it all the way through, then click **Continue**.

### 2. Action to look up the Salesforce Contact ID and Account ID.

This step is needed if you don't reliably maintain the Salesforce Contact ID and Account ID on the SlapFive Member and Company records respectively. It uses the Email to find a matching Salesforce Contact and Company Name to find a matching Salesforce Account.

1. Click the **+** button to add a new step, and on the **2. Action** screen, search for **Salesforce** and select it.
2. On the **Choose app & event** screen, click in the **Choose an event** box, select **Find Record**, and click **Continue**.&#x20;
3. On the **Choose account** screen, select your Connected Account for Salesforce and click **Continue**.
4. On the **Set up action** screen, in the **Salesforce Object** field, select **Contact**, and in the **Field to Search By** field, select **Email**. In the **Search Value** field, select **1. Customer Email: ...** and click **Continue**.
5. On the **Test action** screen, click **Test & Review** to make sure that the Salesforce Account record is found for the SlapFive Member you are using to test this Zap.

### 3. Action to update the Salesforce Account:

1. Click the **+** button to add a new step, and on the **3. Action** screen, search for **Salesforce** and select it.
2. On the **Choose app & event** screen, click in the **Choose an event** box, select **Create Record**, and click **Continue**.&#x20;
3. On the **Choose account** screen, select your Connected Account for Salesforce and click **Continue**.
4. On the **Set up action** screen, in the **Salesforce Object** field, select **Event**.
5. The **Set up action** screen will refresh to show a list of all the Salesforce Event fields. For any fields you want to sync, click within the box under the Salesforce field to select the SlapFive Member field that you want to map to it, or enter a hard-coded value if that’s the update you are looking to make. When done mapping, click **Continue**.
   * [ ] In the **Name** field, select the **2. ID** field.
   * [ ] In the **Related To** field, select the **2. Account ID:** field.
   * [ ] In the **Subject** field, select the **1. Activity Type Name:** field.
   * [ ] In the **Start Date Time** and **End Date Time** fields, select the **1. Date Time:** field.
   * [ ] In the **Description** field, select the **1. Notes:** field.
   * [ ] In the **Type** and **Meeting Activity** fields, select the desired values from the picklists.
6. On the **Test action** screen, click **Test & Review** to test the Zap. Go into Salesforce to verify that the Activity record shows up on both the Account and Contact.
7. If the test is successful, click the **Turn on Zap** button, otherwise check your field mappings.
