---
description: >-
  This page covers how to automate the capture of SlapFive Advocate Status at
  Opportunity Renewal to enable this comparative reporting.
---

# Report on renewal rates for Accounts with advocates vs no advocates

#### Overview

This configuration enables Salesforce to capture whether an Account had an active SlapFive Advocate when a Renewal Opportunity closed.

Currently, the SlapFive Program field on an Opportunity reflects the Account's current participation in SlapFive. As Contacts join or leave the advocacy program, this value can change, making it unsuitable for historical renewal reporting.

The solution is to create a separate Opportunity field that captures Advocate status when the Renewal Opportunity closes and preserves that value for reporting.

**Implementation requirements:**

* One custom Opportunity field
* One Salesforce Record-Triggered Flow
* An update to the renewal reporting dashboard

No modifications to the SlapFive managed package are required.

***

### Step 1: Create the Custom Opportunity Field

1. In Salesforce, click **Setup** (gear icon).
2. Navigate to **Object Manager → Opportunity**.
3. Select **Fields & Relationships**.
4. Click **New**.
5. Select **Picklist** and click **Next**.
6. Enter the following:

| Setting       | Value                 |
| ------------- | --------------------- |
| Field Label   | Advocate at Renewal   |
| Field Name    | Advocate\_at\_Renewal |
| Data Type     | Picklist              |
| Values        | Yes, No, Unknown      |
| Default Value | None                  |
| Required      | No                    |

7. Click **Next**.
8. Set field-level security so the appropriate users can view the field.
9. Make the field read-only for ordinary users if your permissions model allows it. The Flow must still be able to populate it.
10. Add the field to the relevant Opportunity page layouts if desired.
11. Click **Save**.

**Important:** Do not assign a default value. A blank field indicates that the Opportunity has not yet been evaluated.

### Step 2: Create a Record-Triggered Flow

This Flow will automatically populate the new field when a Renewal Opportunity closes.

#### 2.1 Create the Flow

1. Navigate to **Setup → Flows**.
2. Click **New Flow**.
3. Select **Record-Triggered Flow**.
4. Select **Opportunity** as the object.
5. Configure the trigger:

| Setting                | Value                     |
| ---------------------- | ------------------------- |
| Trigger                | A record is updated       |
| Condition Requirements | Formula Evaluates to True |
| Optimize for           | Fast Field Updates        |

Use a formula similar to the following:

```
AND(
  IsClosed,
  NOT(PRIORVALUE(IsClosed)),
  ISPICKVAL(Type, "Renewal"),
  ISBLANK(TEXT(Advocate_at_Renewal__c))
)
```

**Configuration notes:**

* Replace `Renewal` with the exact Opportunity Type value used by your organization.
* If your organization identifies Renewal Opportunities using another field, modify the condition accordingly.
* If Salesforce requires explicit record references in the Flow formula, use `$Record` and `$Record__Prior` references through the formula editor.
* Use the actual API name of the custom field if it differs from the example.

This condition ensures that the Flow runs when an eligible Renewal Opportunity transitions from open to closed and the snapshot field is blank.

#### 2.2 Add a Decision Element

1. Click the **+** icon beneath the Start element.
2. Select **Decision**.
3. Label it **Check SlapFive Program Status**.
4. Create the following outcomes:

**Outcome 1: Member**

Condition:

```
$Record.Account.SlapFive_Program_Status__c = "Member"
```

**Outcome 2: Non-Member**

Condition:

```
$Record.Account.SlapFive_Program_Status__c = "Non-Member"
```

**Default Outcome: Unknown**

Use this when neither condition matches.

**Important:** The field name `SlapFive_Program_Status__c` is illustrative. Use the actual API name of the SlapFive Account field, including its managed-package namespace if applicable.

If Salesforce does not expose the related Account field directly in the Decision element, add a **Get Records** element to retrieve the Account using the Opportunity's AccountId, then evaluate the returned field.

#### 2.3 Add Assignment Elements

For each Decision outcome, create an Assignment element.

**Member outcome**

* Label: Set Advocate at Renewal – Yes
* Variable: `$Record.Advocate_at_Renewal__c`
* Operator: Equals
* Value: `Yes`

**Non-Member outcome**

* Label: Set Advocate at Renewal – No
* Variable: `$Record.Advocate_at_Renewal__c`
* Operator: Equals
* Value: `No`

**Unknown outcome**

* Label: Set Advocate at Renewal – Unknown
* Variable: `$Record.Advocate_at_Renewal__c`
* Operator: Equals
* Value: `Unknown`

Connect each Decision outcome to its corresponding Assignment.

Because this is a before-save Flow, Salesforce will save the assigned value automatically. A separate Update Records element is not required.

### Step 3: Save and Activate the Flow

1. Click **Save**.
2.  Enter:

    **Flow Label:** Capture SlapFive Advocate Status at Renewal

    **Description:** Captures the Account's SlapFive Program Status when a Renewal Opportunity transitions to a closed stage. The resulting snapshot is preserved for historical renewal reporting.
3. Click **Save**.
4. Test the Flow using Salesforce's debugging tools and sandbox test records.
5. Once testing is successful, click **Activate**.

### Step 4: Test the Configuration

Create or identify test Renewal Opportunities in a Salesforce sandbox.

| Test | Account SlapFive Status | Action                                    | Expected Result                     |
| ---- | ----------------------- | ----------------------------------------- | ----------------------------------- |
| 1    | Member                  | Close Renewal as Won                      | Yes                                 |
| 2    | Non-Member              | Close Renewal as Won                      | No                                  |
| 3    | Member                  | Close Renewal as Lost                     | Yes                                 |
| 4    | Non-Member              | Close Renewal as Lost                     | No                                  |
| 5    | Blank                   | Close Renewal                             | Unknown                             |
| 6    | Member                  | Update an open Renewal                    | Remains blank                       |
| 7    | Member                  | Close Renewal, then change Account status | Original snapshot remains unchanged |
| 8    | Member                  | Update an already-closed Renewal          | Original snapshot remains unchanged |
| 9    | Member                  | Close a non-Renewal Opportunity           | Remains blank                       |

Also test an Opportunity whose Close Date is earlier than the date it is actually closed. Confirm that the captured status reflects the Account status when the Flow executes.

### Step 5: Update Renewal Reporting

Once the Flow is active, update the Salesforce report used by the SlapFive renewal dashboard.

1. Open the Salesforce report underlying the renewal-rate dashboard.
2. Confirm that the report includes only eligible Renewal Opportunities with a final Closed Won or Closed Lost outcome.
3. Add the new **Advocate at Renewal** field.
4. Replace grouping or filtering based on the existing **SlapFive Program** Opportunity field with **Advocate at Renewal**.
5. Group results by:
   * Yes — Account had an Advocate when renewal closed
   * No — Account did not have an Advocate when renewal closed
6. Exclude Unknown and blank values from the renewal-rate calculations.
7.  Calculate renewal rates separately for each group:

    **Renewal Rate = Closed Won Renewals ÷ (Closed Won Renewals + Closed Lost Renewals) × 100**
8. Save the report and update the dashboard components.

If the SlapFive dashboard is supplied by the managed package, confirm whether the client can clone and customize the underlying report/dashboard. Some managed-package components may require changes by SlapFive.

### Step 6: Handling Historical Opportunities

The new field will automatically populate only for Renewal Opportunities that close after the Flow is activated.

Historical Renewal Opportunities should not be classified using the Account's current SlapFive Program Status because that may not reflect participation at the time of the historical renewal.

For historical records:

* Leave Advocate at Renewal blank unless historical participation can be verified.
* Set it to Unknown if a populated classification is required.
* Exclude blank and Unknown values from renewal-rate comparisons.

Historical data can be backfilled later if reliable membership history becomes available.

***

### Important Considerations

**Snapshot timing**

The Flow captures Advocate status when Salesforce processes the transition to a closed Opportunity. It does not reconstruct membership based on the Opportunity's Close Date if that date is entered retroactively.

**Data synchronization**

The accuracy of the snapshot depends on the Account's SlapFive Program Status being current when the Flow executes. If membership synchronization is delayed, the snapshot may not reflect the latest SlapFive participation.

**Reopened Opportunities**

This configuration preserves the original snapshot even if an Opportunity is reopened and subsequently closed again. If the organization wants to refresh the snapshot on a subsequent closing, additional Flow logic is required.

**Existing SlapFive fields**

Do not modify the existing SlapFive Program Status field on the Account or SlapFive Program field on the Opportunity. These fields continue to serve their current operational purposes.

### Expected Outcome

After implementation, the renewal dashboard will compare renewal rates based on whether each Account had an Advocate when its Renewal Opportunity closed, rather than whether the Account currently participates in SlapFive.

Historical renewal classifications will remain stable as Advocates join or leave the program.
