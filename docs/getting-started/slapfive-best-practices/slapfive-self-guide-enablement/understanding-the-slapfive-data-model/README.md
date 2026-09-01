---
description: The SlapFive platform is built around connected objects and relationships.
---

# Understanding the SlapFive Data Model

**Core Platform Objects**\
• Members\
• Companies\
• Activities\
• Campaigns\
\
**Why the Data Model Matters**\
Understanding how objects connect improves:\
• Reporting accuracy\
• Workflow automation\
• Search functionality\
• Segmentation\
• Campaign targeting\
\
Designing Your Data Model --> Before creating large numbers of fields, start with the workflows you want SlapFive to support.

Ask: **What decisions do we need this data to help us make?**

For a reference program, you may need:

* Industry
* Company size
* Product
* Use case
* Geography
* Role
* Reference willingness

For a speaker program, you may need:

* Role / Persona
* Speaking willingness
* Topics of expertise
* Geography
* Event participation history

For an advocate sourcing program, you may also want:

* Customer health
* Account tier
* NPS or sentiment
* CSM nomination
* Account owner
* Customer lifecycle stage

This keeps the data model focused on actionable information instead of simply recreating every field from your CRM.

***

## Data Governance Best Practices

### Standardize Naming Conventions

Use consistent field names and terminology across your data model.

For example, avoid having separate fields such as:

* Company Size
* Account Size
* Customer Size
* Segment Size

when they are all intended to represent the same concept.

### Avoid Duplicate Fields

Before creating a new field, determine whether the information already exists elsewhere in the profile.

Duplicate fields can create conflicting data and make filtering unreliable.

### Use Consistent Dropdown Values

Whenever possible, use standardized values rather than unrestricted free-text fields for attributes that will be used for filtering.

For example, instead of allowing:

“United States”\
“USA”\
“U.S.”\
“US”

standardize on one value.

The same principle applies to industries, products, segments, regions, advocacy interests, and other commonly filtered attributes.

### Keep Profile Data Updated

Customer information changes over time.

Account ownership, products, roles, customer status, lifecycle stage, and other attributes should be refreshed regularly—particularly when they originate in another system of record.

### Remove or Deactivate Outdated Records

Establish a process for identifying and managing records that should no longer participate in active advocacy workflows.

***

## Key Takeaway

Your SlapFive data model should be designed around **activation, not data collection.**

Every field should ideally help your team do at least one of the following:

* Find the right advocate
* Match a customer to a request
* Target an audience
* Personalize an advocacy experience
* Understand program coverage
* Measure participation or impact
* Identify gaps in your advocate pool

When profile data is clean, standardized, and connected to your workflows, SlapFive becomes more than a database of advocates—it becomes the system your team can use to **find, activate, and scale the right customer voices at the right time.**

<br>
