---
description: >-
  In this step, you create a Named Credential record that let's Salesforce
  access the SlapFive API.
---

# Create a New Named Credential

#### Overview

This configuration:

* Stores the SlapFive API key securely using an External Credential
* Injects the API key into requests via a custom HTTP header
* Avoids hard-coding secrets in Apex, metadata, or logs

***

### Step 1: Create an External Credential

1. In Salesforce Setup, navigate to **External Credentials**
2. Click **New External Credential**

Use the following values:

* **Label:** SlapFive External API
* **Name:** SlapFiveExternalAPI
* **Authentication Protocol:** Custom

Save the record.

***

### Step 2: Create an External Credential Principal

1. From the External Credential record, create a new **Principal**

Use the following values:

* **Parameter Name (Label):** SlapFive API Key
* **Sequence Number:** 1
* **Identity Type:** Named Principal

2. Under **Authentication Parameters**, add a new parameter:

* **Name:** APIKey
* **Value:** Paste your SlapFive API key here

***

### Step 3: Add a Custom Header to the External Credential

On the same External Credential, add a **Custom Header**:

* **Header Name:** api-authorization
*   **Value:**

    ```
    {!$Credential.SlapFiveExternalAPI.APIKey}
    ```
* **Sequence Number:** 1

This injects the encrypted API key into every request at runtime.

***

### Step 4: Create a Named Credential

1. In Salesforce Setup, navigate to **Named Credentials**
2. Click **New Named Credential**

Use the following values:

* **Label:** SlapFive API
* **Name:** SlapFive\_API
* **URL:** enter the base URL of your SlapFive instance, which is:\
  &#x20;     https://your\_company\_name.slapfive.com.
* **External Credential:** SlapFive External API
* **Generate Authorization Header:** Checked
* **Allow Formulas in HTTP Header:** Checked
* **Allowed Namespaces for Callouts:** slap5

Save the record.

***

### Step 5: Grant Access to the External Credential Principal

Users who need access to the SlapFive App must be granted access to the External Credential Principal. This must be added to every Permission Set that will be assigned to end users, including any cloned copies of the SlapFive managed Permission Set — clones do not inherit External Credential Principal Access automatically.

1. In Salesforce Setup, navigate to **Permission Sets**
2. Open the Permission Set assigned to your end users (e.g. your cloned SlapFive Permission Set)
3. Click **External Credential Principal Access**
4. Click **Edit** and move **SlapFive External API - SlapFive API Key** to the Enabled list
5. Click the Save button
6. Repeat for any additional Permission Sets whose users need SlapFive access

***

### **Step 6: Verify API Access on End User Profiles**

Users that belong to restricted custom Profiles must have the **API Enabled** permission active on their Profile. Without it, Salesforce will block the callouts that the SlapFive component makes, even if their Permission Set is correctly configured.

1. In Salesforce Setup, navigate to **Profiles**
2. Open the Profile assigned to your end users (e.g. Marketing User)
3. Search for **API Enabled** in the profile settings
4. Ensure it is checked
5. Click **Save**
6. Repeat for any additional Profiles whose users need SlapFive access

> ⚠️ **Note:** If end users see the error _"Error retrieving client data: You don't have read permissions on the User external credential object"_, the most likely causes are that Step 5 was not completed for their Permission Set, or that Step 6 was not completed for their Profile.
