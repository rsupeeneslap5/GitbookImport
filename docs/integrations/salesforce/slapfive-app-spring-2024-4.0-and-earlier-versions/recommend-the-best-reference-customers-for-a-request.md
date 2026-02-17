---
description: >-
  This section covers how to enable Salesforce users to see and select from
  recommended reference customers when submitting a Request from a Salesforce
  Opportunity.
---

# Recommend the best reference customers for a Request

## Sample Use Case

Let's say that when your salespeople are asked by a buyer to speak with a reference, they typically want reference customers who are in the same industry and tier as the buyer, and who own the products that the buyer is evaluating.&#x20;

SlapFive enables you to configure the Salesforce App and SlapFive Settings so that your requesters can see a list of recommended Members and/or Companies that are in the same industry and tier, and that own those products. The requester can relax any of those criteria, and add more filter criteria. The requesters can then select from the list of recommended Members and/or Companies to add them to the Request as Fulfillment Company/Member records.

The reference manager can then see and adjust the recommendation criteria, and begin the fulfillment process by reviewing the Companies and/or Members selected by the requester.

## Configure the SlapFive Salesforce App Setup&#x20;

You can configure up to 5 fields from the Salesforce Opportunity and Account records to pass to the Request as recommendation criteria.

1. In Salesforce Setup, go to **Custom Settings**, select **Manage** next to _SlapFive Settings_, and click the **Edit** button.
2. Use the **Matching Field 1, 2, 3, 4 and 5 fields** to specify the Account and/or Opportunity fields to use as recommendation criteria, by entering the _object\_name.field\_name_. Continuing our sample use case, to match on each of these fields, we would enter:
   * [ ] **The Account custom field called Tier:** _Account.Tier\_\_c_
   * [ ] **The Account standard field called Industry:** _Account.Industry_
   * [ ] **The Products specified on the Opportunity:** _OpportunityLineItem.Product_
3. Click the **Save** button.

## Configure the SlapFive Settings

In SlapFive **Client Settings**, you specify whether you want the requesters to see recommended Members, Companies, or both, and you connect the **Matching Fields 1..5** that you specified in Salesforce to the corresponding objects and fields in SlapFive.

1. In your SlapFive **Client Settings**, click the **Basic Settings** tab and scroll down until you see these two fields.&#x20;
   * [ ] **Allow Requesters to Select Companies:** Check this box if you want requesters to see recommended Companies.
   * [ ] **Allow Requesters to Select Members:** Check this box if you want requesters to see recommended Members. Few SlapFive clients select this option.
2. Click the **Search Settings** tab.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-11-18 084615.png" alt=""><figcaption><p>Search Settings tab</p></figcaption></figure>

3. In the **Salesforce Search Filters for New Requests** section, you will add a Search Filter for each Matching Field 1..5 you defined in Salesforce Setup. Click the **Add** button, enter the values as follows and click the **Save** button:

<figure><img src="../../../.gitbook/assets/Screenshot 2024-11-18 091134.png" alt=""><figcaption><p>Add Search Filter tray.</p></figcaption></figure>

* [ ] **Entity:** Select the object that contains the field you want to match, in this case _Company_.
* [ ] **Field:** Select the field you want to match, in this case _Size_.
* [ ] **Comparison:** Select _equals_.
* [ ] **Value:** Select any value for this field that you want to be the default should the Salesforce Opportunity or Account not have a value for this field.
* [ ] **Salesforce Input Order:** Set this number to the corresponding Matching Field number in Salesforce Client Settings. In this case we are mapping this to **Matching Field 1**, so we select _1_.

4. Repeat Step 3 for each Matching Field 1..5.
