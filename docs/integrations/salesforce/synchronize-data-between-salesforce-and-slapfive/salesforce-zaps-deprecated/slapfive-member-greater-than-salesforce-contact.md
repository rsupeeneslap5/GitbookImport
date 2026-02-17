---
description: >-
  This Zap keeps a Salesforce Contact up to date when changes are made to a
  corresponding SlapFive Member.
---

# SlapFive Member > Salesforce Contact

While logged into your Zapier account, click the **Create Zap** button.

### 1. Trigger to listen for a new or changed Member in SlapFive:

1. On the **1. Trigger** screen, name your Zap in the upper left, then in the **Search apps…** box, search for **SlapFive**, and select it.
2. In the **Choose an event** box, select **New or Changed Member** and click **Continue**.
3. On the **Choose account** screen, select your Connected Account for SlapFive and click **Continue**.
4. Click the **Test trigger** button to pull some data into the Zap so you can test it all the way through, then click **Continue**.

### 2. Action to get all the Member fields for the Customer so you can send them to Salesforce.

This step is only needed if you want to get more than the Member base fields that are retrieved in Step 1, such as the Industry and Location fields on the Member Company.

1. On the **2. Action** screen, search for **SlapFive** and select it.
2. On the **Choose app & event** screen, in the Action Event box, click **Find Record**, and click **Continue**.&#x20;
3. On the **Choose account** screen, select your Connected Account for SlapFive and click **Continue**.
4. On the **Set up action** screen, in the **SlapFive Object** field, select **Member**, and in the **ID** field, select **1. ID: …** and click **Continue**.
5. On the **Test action** screen, click **Test & Review** and make sure that the record is found for the SlapFive Member you are using to test this Zap.

### 3. Action to look up the Salesforce Contact ID.

This step is needed if you don't reliably maintain the Salesforce Contact ID on the SlapFive Member records. It uses the Member's Email to find a matching Salesforce Contact.

1. Click the **+** button to add a new step, and on the **3. Action** screen, search for **Salesforce** and select it.
2. On the **Choose app & event** screen, click in the **Choose an event** box, select **Find Record**, and click **Continue**.&#x20;
3. On the **Choose account** screen, select your Connected Account for Salesforce and click **Continue**.
4. On the **Set up action** screen, in the **Salesforce Object** field, select **Contact**, and in the **Field to Search By** field, select **Email**. In the **Search Value** field, select **1. Email: ...** and click **Continue**.
5. On the **Test action** screen, click **Test & Review** to make sure that the Salesforce Contact record is found for the SlapFive Member you are using to test this Zap.

### 4. Action to update the Salesforce Contact:

1. Click the **+** button to add a new step, and on the **4. Action** screen, search for **Salesforce** and select it.
2. On the **Choose app & event** screen, click in the **Choose an event** box, select **Update Record**, and click **Continue**.&#x20;
3. On the **Choose account** screen, select your Connected Account for Salesforce and click **Continue**.
4. On the **Set up action** screen, in the **Salesforce Object** field, select **Contact**, and in the **Record to Update** field, click the **Custom** tab and then select the **3. ID ...** field.
5. The **Set up action** screen will refresh to show a list of all the Salesforce Contact fields. For any fields you want to sync, click within the box under the Salesforce field to select the SlapFive Member field that you want to map to it, or enter a hard-coded value if that’s the update you are looking to make. When done mapping, click **Continue**.&#x20;
6. On the **Test action** screen, click **Test & Review** to test the Zap. Go into Salesforce to verify that the Contact record was updated properly.
7. If the test is successful, click the **Turn on Zap** button, otherwise check your field mappings.
