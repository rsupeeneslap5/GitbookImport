---
description: >-
  With this integration, Customer Referrals captured in Eloqua forms create
  Activities, Referral Tracking, and Revenue Influence in SlapFive.
---

# Customer Referrals

SlapFive has greatly simplified the process and dataflow for gathering customer referrals. The best part is that we use your Marketing Automation platform to build the Referral Form, which has several advantages:

* Accessing the Referral Form doesn't require your customers to log in to an app or portal, so any customer can submit a referral, not just your advocates.
* You can link to the Referral Form from anywhere, including your customer community, customer newsletters, email campaigns, blog posts.
* Your Referral Form automatically creates a Lead/Contact record in your Marketing Automation platform so there's no integration required between the two.
* It takes advantage to the configuration you already have in place for your Marketing Automation platform to create Salesforce Lead records.

## Customer Referrals Workflow and Dataflow

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-13 195939.png" alt=""><figcaption><p>Customer Referrals Workflow and Dataflow</p></figcaption></figure>

## How to set it up:

1. Create the Referral Form in your Marketing Automation platform. Include fields for the Referral's First Name, Last Name, Title, Email, Phone, Company, and Referral Reason, along with fields for the Referred by Customer's Email. Your SlapFive CSM will provide you with a shared Google Sheet for capturing all the field names from the form and their corresponding fields in your Marketing Automation platform.
2. In SlapFive, connect to your Eloqua environment as [described here](connect-to-eloqua.md), and connect to your Salesforce org as [described here](../salesforce/synchronize-data-between-salesforce-and-slapfive/connect-to-salesforce.md). Let your SlapFive CSM know when you are connected to both.
3. SlapFive sets up these integration points:
   * [ ] When a new Referral Form completion creates a Lead/Contact in Eloqua, create a Member record if one doesn't exist for the Referred by Customer, create an Activity History record for the Referred by Customer and add a new row to the Referral Tracker in SlapFive.
   * [ ] When the Salesforce Lead gets converted to an Opportunity, update the Referral Tracker in SlapFive, create the SlapFive Customer Influence record in Salesforce.
   * [ ] Each time the Salesforce Opportunity's Stage is changed, update the Referral Tracker in SlapFive.
   * [ ] Log additional Activity History records for the Referred by Customer at your desired milestones and optionally have these trigger the sending of a gift or token of appreciation to that Customer.
