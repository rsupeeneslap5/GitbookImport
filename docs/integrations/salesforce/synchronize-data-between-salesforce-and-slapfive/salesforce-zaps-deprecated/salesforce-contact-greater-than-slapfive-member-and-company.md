---
description: >-
  This Zap keeps a SlapFive Member and Company up to date when changes are made
  to a corresponding Salesforce Contact.
---

# Salesforce Contact > SlapFive Member & Company

While logged into your Zapier account, click the **Create Zap** button.

### 1. Trigger for change to Salesforce Contact:

1. On the **1. Trigger** screen, name your Zap in the upper left, then in the **Search apps…** box, search for **Salesforce**, and select it.
2. In the **Choose an event** box, select **Updated Field on Record** and click **Continue**.
3. On the **Choose account** screen, select your Connected Account for Salesforce and click **Continue**.
4. On the **Set up trigger** screen, select the Salesforce **Contact** object and click **Continu**e.
5. Click the Test trigger button to pull some data into the Zap so you can test it all the way through, then click **Continue**.

### 2. Action to create or update SlapFive Member & Company:

{% hint style="info" %}
This Action first uses a Salesforce Contact ID to see if a Member already exists with that ID. If no match is found it will then use the Email Address to see if a Member already exists with that Email. If either match, it will update the existing Member, otherwise it will create a new Member.

This Action also first uses a Salesforce Account ID to see if a Company already exists with that ID. If no match is found it will then use the Account Name to see if a Company already exists with that name. If either match, it will update the existing Company, otherwise it will create a new Company.
{% endhint %}

1. On the **2. Action** screen, search for **SlapFive** and select it.
2. On the **Choose app & event** screen, click in the **Choose an event** box, select **Create or Update Customer**, and click **Continue**.&#x20;
3. On the **Choose account** screen, select your Connected Account for SlapFive and click **Continue**.
4. On the **Set up action** screen, you will see a list of all the SlapFive fields for a customer’s Member and Company records. Click within the box under each SlapFive field to select the Salesforce field that you want to map to it. See the help text under each box for more information about that field, and the required fields are noted. When done mapping, click **Continue**.
5. On the **Test action** screen, click **Test & Review** to test the Zap. Go into SlapFive to verify that the customer’s Member record was updated properly.
6. If the test is successful, click the **Turn on Zap** button, otherwise check your field mappings.
