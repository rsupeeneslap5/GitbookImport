---
description: >-
  This page gives you the steps to take when you receive the Connection Failed -
  Action failed due to server error when trying to connect SlapFive/Workato to
  Salesforce.
---

# Connection Failed - Action failed due to server error

### The most likely cause

When Workato tries to connect to Salesforce but only shows **“Connection Failed – Action failed due to server error,”** 90% of the time it means Salesforce is blocking Workato from signing in. Here’s what you need to do.

Go to **Setup → Connected Apps → Connected Apps OAuth Usage.**

You’ll see a list of Connected App that users have recently authenticated with. Look for one of the following:

* **Workato**
* **Workato connector**
* **Workato OAuth Connector**

Salesforce does not literally put a red “Blocked” label here. Instead, a Connected App becomes effectively blocked when the app is restricted to “Admin approved users only”. This blocks the Integration User unless they're explicitly granted access.

#### **How to unblock:**

1. In the **Workato connector** row, click the **Manage App Policies** link.
2. Scroll to the **OAuth Policies** section and look at the **Permitted Users** field. If it says:

**“Admin approved users are pre-authorized”**

…then Salesforce is blocking Workato for all users who haven’t been assigned. To unblock it for your Integration User, there are two options:

#### Option 1 — Assign via Permission Set

1. Go to **Setup → Permission Sets**
2. Open the Permission Set used for API integrations
3. Click **Assigned Connected Apps**
4. Add **Workato connector**
5. Assign the Permission Set to the Integration User

#### Option 2 — Assign via Profile

1. Go to **Setup → Profiles**
2. Open the Integration User’s profile
3. Scroll to **Connected App Access**
4. Check the box next to **Workato connector**
5. Click Save

Once assigned, Workato is unblocked for that user.

If this doesn't eliminate the error, continue below.

***

### **Other possible causes**

The other 10% of the time that error appears, it is something more obscure. Here are the things to check, in order of likelihood.

#### **1. Confirm the Workato Connected App is installed**

Go to **Setup → Connected Apps → Manage Connected Apps**

Check that one of these appears in the list:

* **Workato connector**
* **Workato**
* **Workato OAuth Connector**

If the Workato app does not appear, the connection will fail.

**Fix:**\
You’ll need to install the Workato managed package so the Connected App becomes visible and assignable.

#### **2. Verify that the Integration User has the right permissions**

Salesforce only issues API tokens when the user has the necessary permissions.

Confirm the Integration User has:

* **API Enabled**
* **Access to the objects and fields** [shown here](../../synchronize-data-between-salesforce-and-slapfive/determine-the-salesforce-integration-user.md).

Missing object access or Record Type assignments commonly trigger this error.

#### **3. Check if your org is blocking non-installed Connected Apps**

Some Salesforce orgs enforce a security policy that blocks Connected Apps that are not explicitly installed in the org.

If this setting is active:

* Workato’s standard Connected App will be blocked
* You will see connection failures with no detailed error message

**Fix:**\
Install the **Workato Installed Package**, which adds an org-local version of the Workato Connected App that Salesforce will trust.

#### **4. Make sure Workato is connecting to the correct domain**

If your Salesforce org recently enabled **My Domain** or adopted **Enhanced Domains**, older connection settings no longer work.

**Fix:**\
Reconnect the Workato connection using your My Domain URL, for example:\
`https://yourdomain.my.salesforce.com`

***

#### **5. Check for IP restrictions or token policies**

If your org uses strict login or token policies, Salesforce may block Workato’s login attempt.

Please check:

* **Setup → Login Access Policies**
* **Setup → Network Access** (Trusted IP ranges)
* **Connected App Session Policies** for the Workato app

If Workato’s IP ranges are not trusted or token policies are too strict, OAuth login will fail.

#### **6. Refresh the connection in Workato**

Sometimes the simplest fix works:

1. Go to the Workato connection
2. Click **Reconnect**
3. Re-enter the credentials for the Integration User
4. Make sure your browser does not block the Salesforce login popup

This forces Salesforce to issue a fresh OAuth token.

#### **7. If the issue persists: capture the Salesforce Login History**

In Salesforce:

**Setup → Users → Integration User → Login History**

Look at the most recent failed login entry. The error code there (for example, _invalid\_grant_, _IP restricted_, _user hasn’t approved this app_) will tell us exactly what Salesforce is rejecting.

Send us that line and we can pinpoint the fix instantly.
