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

### Integration User Permissions

The Embedded Integration with Salesforce requires you to establish a Salesforce Connection using a Salesforce Integration User with these permissions:

<table><thead><tr><th width="226">Object</th><th width="146">Permssion Type</th><th>Permission</th></tr></thead><tbody><tr><td>Opportunity</td><td>Object-level</td><td>Read</td></tr><tr><td></td><td>Field-level</td><td>Read access to any Opportunity fields we need to retrieve and pass to SlapFive, such as Stage or Amount. Remove any field validation rules defined for the Salesforce Opportunity object for this user. <br>Example: "You cannot move this Opportunity to Stage 2 without selecting a Meeting Outcome". </td></tr><tr><td></td><td>Record-level</td><td>Access to any Opportunity records that may have influence events associated with it.</td></tr><tr><td>Account</td><td>Object-level</td><td>Read</td></tr><tr><td></td><td>Field-level</td><td>Read access to any Account fields we need to monitor for changes, retrieve and pass to SlapFive, such as Industry or Size.</td></tr><tr><td></td><td>Record-level</td><td>Access to any Account records that may be synced with SlapFive.</td></tr><tr><td>Contact</td><td>Object-level</td><td>Read</td></tr><tr><td></td><td>Field-level</td><td>Read access to any Contact fields we need to monitor for changes, retrieve and pass to SlapFive, such as Title or LinkedIn Profile.</td></tr><tr><td></td><td>Record-level</td><td>Read access to any Contact records that may be synced with SlapFive.</td></tr><tr><td>SlapFive Customer Influence, SlapFive Customer Influence Activity, SlapFive Customer Activity Objects</td><td>Object-level</td><td>Read, Create, Edit, Delete</td></tr><tr><td></td><td>Field-level</td><td>Read and Edit access to all fields</td></tr><tr><td></td><td>Record-level</td><td>Access to all records.</td></tr></tbody></table>

In addition, the Integration User needs access to the setup objects used by the SlapFive Salesforce App:

* [ ] The Named Credential with Name = SlapFive\_API
* [ ] The SlapFive Settings object
* [ ] The SlapFive Connected App

### Restrict Integration User to IP addresses or ranges

If your company requires your Salesforce Integration User to be restricted to specific IP addresses or ranges, your Salesforce Admin needs to add these IP Addresses to the **Login IP Ranges** for the Integration User:

* [ ] 52.5.142.59
* [ ] 34.226.132.221
* [ ] 52.54.43.157
