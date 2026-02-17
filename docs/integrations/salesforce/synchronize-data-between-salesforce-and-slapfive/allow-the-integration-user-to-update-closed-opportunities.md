---
description: >-
  This section covers how to set up Salesforce so that the SlapFive Revenue
  Influence Reporting automations can update closed Salesforce Opportunities.
---

# Allow the integration user to update closed Opportunities

### Why this may be needed

The Revenue Influence Reporting in the SlapFive Salesforce App uses the [custom objects SlapFive Customer Influence and SlapFive Customer Influence Activity](https://docs.slapfive.com/integrations/salesforce#custom-objects), as well as the [Opportunity custom fields described here](https://docs.slapfive.com/integrations/salesforce#custom-fields). It is not uncommon for revenue influence events to be recorded after the Opportunity has been closed. If your company has an Opportunity Validation Rule that prevents any updates to closed Opportunities, then the SlapFive integration cannot create or update the custom objects. The solution is to modify the Opportunity Validation Rule to allow thd Integration User to update closed Opportunities.

### Add an Automation Bypass to the Opportunity Validation Rule

Modify the existing Opportunity validation rule to **exclude trusted automation**, such as an integration user or permission set.

#### Step 1: Create a Permission Set

1. Go to **Setup → Permission Sets**
2. Click **New**
3. Name it something like:
   * `Bypass Closed Opportunity Validation`
4. Save

No object permissions are required.

#### Step 2: Update the Validation Rule

Edit the existing Opportunity Validation Rule and add a condition to exclude users with this permission set.

**Example logic:**

```
AND(
  IsClosed = TRUE,
  NOT($Permission.Bypass_Closed_Opportunity_Validation)
)
```

This means:

* The rule still blocks edits to closed Opportunities
* Except when the user has the bypass permission

#### Step 3: Assign the Permission Set

Assign the permission set to your integration user.
