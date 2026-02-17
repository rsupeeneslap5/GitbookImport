---
description: >-
  If you want to use Okta to provide Single Sign-On access to SlapFive, you need
  to do these steps.
---

# Use Okta for Single Sign-On

{% hint style="info" %}
NOTE: These instructions describe how to set up the SlapFive app in Okta in the most standard way. If your company has configured Okta in more advanced ways, you will need to go to Okta for support on how set up this SSO.
{% endhint %}

## Configure Okta Groups and SlapFive Roles

To have Okta assign each Okta User to a specific SlapFive Role, you need to set up a SlapFive Role with a name that exactly matches each Okta Group being used for accessing SlapFive.

* [ ] Determine the Okta Groups you'll use and make sure each Okta User who you want to have access to SlapFive belongs to one of those Groups. If you want dedicated Okta Groups for granting SlapFive access, we suggest giving them a prefix like _SlapFive-CSM_.
* [ ] Create each SlapFive Role and assign the appropriate **Entity Access** and **Filters** as described in the [Configure Role-Based Permissions](configure-role-based-permissions.md) section.

## Create the Okta Application

In Okta, create a new **Application** for SlapFive.

* [ ] In the **Platform** field, select **Web**.
* [ ] In the **Sign On Method** field, select **SAML** and click **Create**.
* [ ] In the **App name** field, enter **SlapFive**.
* [ ] If you'd like to upload an **App logo**, save this one and upload it, and click **Next**:![](../.gitbook/assets/slapfive_logo_full.png)
* [ ] In the **Single sign on** **URL** field, paste the URL **https://auth.slapfive.com/login/callback?connection=**_**instance**_**-sso**, and substitute your SlapFive instance name for _instance._ Don't forget the **-sso** at the end.
* [ ] Check the **Use this for Recipient URL and Destination URL** field.
* [ ] In the **Audience URL (SP Entity iD)** field, paste **urn:auth0:slapfive:**_**instance**_**-sso**, and substitute your SlapFive instance name for _instance_.
* [ ] Scroll down to the **Attribute Statements (optional)** section and enter these three attributes:

<figure><img src="../.gitbook/assets/Screen Shot 2023-01-19 at 4.45.20 PM.png" alt=""><figcaption></figcaption></figure>

* [ ] Generate a **SAML Signing Certificate** for the SlapFive App Integration.
* [ ] For the question **Are you a customer or a partner?** choose **I'm an Okta customer adding an internal app**. Scroll to the bottom and click **Finish**.
* [ ] In the **Group Attribute Statements (optional)** section, create an attribute as follows:
  * [ ] **Name:** groups
  * [ ] **Name format (optional):** Unspecified
  * [ ] **Filter:** use a filter criteria that will access the Okta Groups. If you gave each Okta Group a prefix of SlapFive-, then set the filter criteria to _Starts with_, _SlapFive-_.
* [ ] Click the **Assignments** tab where you can add People and/or Groups who need access to SlapFive.
* [ ] Click the **Sign On** tab, then click the **View Setup Instructions** button. A new page will open where you'll find the **Identity Provider Single Sign-On URL**. It will look like this:\
  &#x20;       **http://www.okta.com/**_**YOUR-COMPANY-NAME**_**/exkkmadrisATGCYEd307/sso/saml**&#x20;
* [ ] Click **Download Certificate** to save the _**X.509 Certificate**_.&#x20;
* [ ] Send the **Identity Provider Single Sign-On URL** and the **X.509 Certificate** to your SlapFive coach so we can load them into SlapFive's authentication server.
* [ ] We will let you know when those updates are made so you can test the login.

