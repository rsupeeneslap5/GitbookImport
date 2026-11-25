---
description: >-
  This section describes the access permissions required for the Salesforce user
  that you will use to authenticate to Salesforce.
---

# Determine the Salesforce integration user

### Authentication Type

The integration uses OAuth 2.0 Authentication.

### How the Connection to Salesforce is Established

1. In SlapFive Settings, you click **Integrations > Salesforce Connection**,  then click the **Connect** button.
2. The Integration Server redirects you to the Salesforce login page, where you log in as your **Integration User**, typing the username and password.
3. Salesforce authenticates you and asks for consent.
4. Salesforce issues two tokens:
   1. **Access Token** - short-lived, used to make API calls.
   2. **Refresh Token** - long-lived, used to  get new access tokens when the old one expires.
5. The Integration Server stores the Access Token and Refresh Token encrypted in its vault.&#x20;

{% hint style="info" %}
NOTE: No usernames or passwords are ever stored in SlapFive. The Integration Server uses the Refresh Token to silently refresh Access Tokens in the background, without needing the password again.
{% endhint %}

### Object-level Integration User Permissions

The Embedded Integration with Salesforce requires you to establish a Salesforce Connection using a Salesforce Integration User with these permissions:

<table><thead><tr><th width="226">Object</th><th width="146">Permssion Type</th><th>Permission</th></tr></thead><tbody><tr><td>Opportunity</td><td>Object-level</td><td><p><strong>Read, Edit, View All Records</strong></p><p></p><ul><li><strong>Edit</strong> is needed to update the four custom Opportunity fields. SlapFive does not update any other fields.</li><li><strong>View All Records</strong> is needed for any automated workflows that listen for specific field changes on Opportunities, such as the referral automation. If not granted, the Integration User must have record-level visibility to every Opportunity that may be synchronized with or monitored by SlapFive.</li></ul></td></tr><tr><td></td><td>Field-level</td><td><ul><li><strong>Read and Edit</strong> access to the four SlapFive custom fields: Influence Count, SlapFive Influence, SlapFive Influence Score, and SlapFive Program.</li><li><strong>Read</strong> access to all fields referenced by the SlapFive integration, including any fields configured for synchronization or monitoring: Opportunity Name, Id, Description, Stage, Is Closed, Is Won, Amount, Created Date, Close Date, Type, Lead Source, Account ID.</li></ul></td></tr><tr><td></td><td>Record-level</td><td><strong>Read</strong> access to every Opportunity that may be synchronized with or monitored by SlapFive, and <strong>Read/Write</strong> access to every Opportunity that SlapFive may update.</td></tr><tr><td></td><td>Opportunity Validation Rules</td><td><p>Ensure that Salesforce Opportunity validation rules do not prevent the Integration User from updating the four SlapFive custom Opportunity fields.</p><p></p><p>Where necessary, configure an exception for the Integration User in applicable validation rules, preferably using a Custom Permission assigned through a Permission Set.</p><p></p><p>Example: "You cannot move this Opportunity to Stage 2 without selecting a Meeting Outcome." </p></td></tr><tr><td>Account</td><td>Object-level</td><td>Read, View All</td></tr><tr><td></td><td>Field-level</td><td>Read access to all fields referenced by the SlapFive integration, including any fields configured for synchronization or monitoring, such as Industry or Size.</td></tr><tr><td></td><td>Record-level</td><td><strong>View All</strong> object permission is recommended. If not granted, the Integration User must have record-level visibility to every Account that may be synchronized with SlapFive.</td></tr><tr><td>Contact</td><td>Object-level</td><td>Read, View All</td></tr><tr><td></td><td>Field-level</td><td>Read access to all fields referenced by the SlapFive integration, including any fields configured for synchronization or monitoring, such as Title or LinkedIn Profile.</td></tr><tr><td></td><td>Record-level</td><td><strong>View All</strong> object permission is recommended. If not granted, the Integration User must have record-level visibility to every Contact that may be synchronized with SlapFive.</td></tr><tr><td><p>SlapFive Customer Influence</p><p></p><p>SlapFive Customer Influence Activity</p><p></p><p>SlapFive Customer Activity</p><p></p><p>SlapFive Board</p><p></p><p>SlapFive Company</p><p></p><p>SlapFive Contact</p><p></p><p>SlapFive Story</p></td><td>Object-level</td><td>Read, Create, Edit, Delete for Admins and program owners, Read for all others.</td></tr><tr><td>SlapFive Customer Influence</td><td>3 Record Types</td><td>Read and Edit</td></tr><tr><td>SlapFive Customer Influence Activity</td><td>3 Record Types</td><td>Read and Edit</td></tr><tr><td></td><td>Field-level</td><td>Read and Edit access to all fields</td></tr><tr><td></td><td>Record-level</td><td>Access to all records.</td></tr></tbody></table>

### System-level Integration User Permissions

The Integration User needs these system permissions to enable the real-time listening for Opportunity, Account and Contact record changes to sync to SlapFive, as this uses Salesforce Change Data Capture (CDC) to listen for Salesforce change events, which requires CDC registration:

* [ ] API Enabled
* [ ] View Setup and Configuration
* [ ] Customize Application
* [ ] Manage Flow
* [ ] Flow User
* [ ] Salesforce API Integration permission set license
* [ ] View All permission for the object (Contact, Account, Opportunity)

In addition, the Integration User needs access to the setup objects used by the SlapFive Salesforce App:

* [ ] Named Credential with Name = SlapFive\_API
* [ ] SlapFive Settings object
* [ ] SlapFive Custom Metadata Types
* [ ] Assigned the SlapFive API Permission Set

### Restrict Integration User to IP addresses or ranges

If your company requires your Salesforce Integration User to be restricted to specific IP addresses or ranges, your Salesforce Admin needs to add these IP Addresses to the **Login IP Ranges** for the Integration User:

* [ ] 52.5.142.59
* [ ] 34.226.132.221
* [ ] 52.54.43.157
