---
description: >-
  When you invite people from other teams like Demand Gen and Customer Success
  to use SlapFive, you'll want to configure which functions and data they should
  see. This section explains how to do it.
---

# Configure Role-Based Permissions

SlapFive enables you to define Roles, assign Users to Roles, and determine which menu options and data that Users in each Role have permission to see and edit.&#x20;

SlapFive comes pre-configured with these two Roles:

* **Admin:** this is the default role for new Users you invite to SlapFive, and is used for members of your core team who need access to all SlapFive modules and data.
* **Viewer:** this role is automatically assigned to any users who access SlapFive content and features from within the SlapFive Salesforce App.

SlapFive enables you to define these two levels of permissions for each Role:

* **Access:** What level of access do Users have to each Entity on the SlapFive menu? Sample use cases:
  * [ ] Marketing users should be able to view Members and Companies and edit Stories and Boards.
  * [ ] Customer Success users should be able to edit Members and Companies and view Stories and Boards.
* **Filters:** What filters should be applied to the data that Users can see when accessing each Entity? If you define multiple filters for different fields for the same entity, AND logic is applied so that the records the user can see must meet all filter criteria. Sample use cases:
  * [ ] Marketing users should only see Members and Companies who are active members of your program. For the Members entity, you may only want to show Members where both the Member and their Company record are Active. So for the Member entity, you'd define a filter for Member **Active Status** = _Active_ and Company **Active Status** = _Active_. Then for the Company entity, you'd define a filter for Company **Active Status** = _Active_.
  * [ ] Customer Success users should see Stories that have been released for use and not any that are work-in-process. So for the Stories entity, you'd define a filter for Story **Status** = _Released_.

### Define and configure a new Role

Create a new Role for each department or function from which you want to invite people to access SlapFive and who's members share the same permissions. To create a new Role, follow these steps:

1. Log into SlapFive and go to **Admin menu** > **Roles**.
2. Click the **Add Role** button, enter the name for the new Role, click the **OK** button and you will see a list of Entities which correspond to SlapFive menu options.
3. Under the **Access** column, each Entity has a drop-down field with different access levels. Select which access level to grant Users in this Role from these choices:
   * [ ] **Edit:** Users can view, create, and edit.
   * [ ] **View:** Users can view, but not create or edit.
   * [ ] **None:** Users cannot view this menu item or data for this Entity.
4. Under the **Filters** column, each Entity has a (+) button that allows you to apply filters to the data that Users in this Role can see. To add a new filter, select values for each of these fields and then click the **Save** button:
   * [ ] **Entity:** Select the Entity from which you want to select fields to apply filters.
   * [ ] **Field:** Based on the Entity selected, you will see Fields for that Entity. Select which Field you to which want to apply a filter.
   * [ ] **Comparison:** Leave the default value of Equals. SlapFive will be adding more Comparison operators over time.
   * [ ] **Value:** Based on the Entity and Field selected, you will see values for that Field. Select which value you'd like to use in the filter.
5. Click the **Save** button to save the Role.

Here is an example of a Marketing Role that has been defined with Access and Filter permissions:

<figure><img src="../.gitbook/assets/Screenshot 2024-10-31 083146.png" alt=""><figcaption><p>Create or Edit a Role screen</p></figcaption></figure>
