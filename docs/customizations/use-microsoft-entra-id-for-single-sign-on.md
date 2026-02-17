---
description: >-
  If you want to use Microsoft Entra ID (formerly Azure Active Directory) to
  provide Single Sign-On access to SlapFive, you need to do these steps.
---

# Use Microsoft Entra ID for Single Sign-On

{% hint style="info" %}
NOTE: These instructions describe how to set up the SlapFive app in Entra ID in the most standard way. If your company has configured Entra ID in more advanced ways, you will need to go to Microsoft for support on how set up this SSO.
{% endhint %}

## Configure Entra ID App Roles and SlapFive Roles

To have Entra ID assign each User to a specific SlapFive Role, you need to set up your SlapFive Roles with names that exactly match each Entra ID App Role being used for accessing SlapFive.

* [ ] Determine the Entra ID App Roles you'll use and make sure each Entra ID User who you want to have access to SlapFive belongs to one of those App Roles. If you want dedicated App Roles for granting SlapFive access, we suggest giving them a prefix like _SlapFive-CSM_.
* [ ] Create each SlapFive Role and assign the appropriate **Entity Access** and **Filters** as described in the [Configure Role-Based Permissions](configure-role-based-permissions.md) section.

## Create the Entra Application

In Azure, go to **Enterprise Applications > New Application > Create your own application**.

* [ ] Under the **What are you looking to do with your application?** section, choose the **Non-gallery application** option.
* [ ] Name your application _**SlapFive**_ and then add it.
* [ ] Go to **Azure Active Directory > Enterprise applications** and open the newly created _**SlapFive**_ application.
* [ ] Select the **Single sign-on** tab, and then choose **SAML** as the sign-on method.
* [ ] On the **Configure App Settings** page, enter the following:
  * [ ] **Identifier (Entity ID):** Paste **urn:auth0:slapfive:**_**instance**_**-sso**, and substitute your SlapFive instance name for _instance_. Don't forget the **-sso** at the end.
  * [ ] **Reply URL (Assertion Consumer Service URL):** paste the URL **https://auth.slapfive.com/login/callback?connection=**_**instance**_**-sso**, and substitute your SlapFive instance name for _instance._ Don't forget the **-sso** at the end.
  * [ ] **Sign on URL (Optional):** Do not set.
  * [ ] **Relay State (Optional):** Do not set.
* [ ] On the **Configure App Settings** page, find the **SAML Signing Certificate** section.
* [ ] Locate the **XML download link** under the [Federation Metadata URL](https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/configure-saml-single-sign-on#saml-signing-certificate), and download the file.
* [ ] Send the file and the **Single Sign-On URL** to your SlapFive coach so we can load them into SlapFive's authentication server. We will let you know when those updates are made so you can test the login.
* [ ] Add Users to the _**SlapFive**_ app.
