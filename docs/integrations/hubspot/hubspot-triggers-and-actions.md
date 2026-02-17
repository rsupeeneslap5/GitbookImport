---
description: >-
  This section covers what HubSpot events can trigger an interation or workflow,
  and what actions can happen in HubSpot triggered by SlapFive and other apps.
---

# HubSpot Triggers & Actions

With SlapFive's integration and automation server, you can implement any automated workflow you can envision. To help you understand what's possible, here are the HubSpot Triggers that we can listen to for initiating an automated workflow, as well as the Actions that are available when workflows are triggered from HubSpot, SlapFive, or any other system.

### Triggers

SlapFive can listen and take action on any of these HubSpot Trigger events.

| Trigger                    | Description                                                                                                                   |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| New/updated record         | Triggers when a record for any HubSpot object is created or updated. This includes the Contact, Company, Deal, Product, List. |
| New/updated record - batch | Retrieves records for any HubSpot object that are new or updated since the last batch job.                                    |
| New Form submission        | Triggers whenever a specified HubSpot form is submitted.                                                                      |
| New Contact in List        | Triggers whenever a Contact is added to a specified HubSpot List.                                                             |

### Actions

SlapFive can take these Actions in HubSpot whenever an integration or automated workflow is triggered in HubSpot, SlapFive, or any other app.

| Action                            | Description                                                                                                                                                     |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Create or update a record         | Use data from a prior step to create a new record or update an existing record for any HubSpot object. This includes the Contact, Company, Deal, Product, List. |
| Create or update records in batch | Use data from a prior step to create or update many records in batch.                                                                                           |
| Create Engagement                 | Create an Engagement record in HubSpot.                                                                                                                         |
| Add Contact to List               | Add a Contact to a specified List.                                                                                                                              |
| Add Contact to Workflow           | Add a Contact to a specified Workflow in HubSpot.                                                                                                               |
| Import CRM Data                   | Bulk upload data to HubSpot                                                                                                                                     |
| Search record                     | Search for records for any object using search criteria.                                                                                                        |
| Associate records                 | Associate a record from one object to another object.                                                                                                           |
