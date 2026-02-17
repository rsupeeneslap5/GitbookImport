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

#### Step 1: Create an External Credential

1. In Salesforce Setup, navigate to **External Credentials**
2. Click **New External Credential**

Use the following values:

* **Label:** SlapFive External API
* **Name:** SlapFiveExternalAPI
* **Authentication Protocol:** Custom

Save the record.

***

#### Step 2: Create an External Credential Principal

1. From the External Credential record, create a new **Principal**

Use the following values:

* **Parameter Name (Label):** SlapFive API Key
* **Sequence Number:** 1
* **Identity Type:** Named Principal

2. Under **Authentication Parameters**, add a new parameter:

* **Name:** APIKey
* **Value:** Paste your SlapFive API key here

***

#### Step 3: Add a Custom Header to the External Credential

On the same External Credential, add a **Custom Header**:

* **Header Name:** api-authorization
*   **Value:**

    ```
    {!$Credential.SlapFiveExternalAPI.APIKey}
    ```
* **Sequence Number:** 1

This injects the encrypted API key into every request at runtime.

***

#### Step 4: Create a Named Credential

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
* **Allowed Namespaces for Callouts:** SlapFiveInc

Save the record.

***

#### Step 5: Grant Access to the External Credential Principal

Users running SlapFive automations must be granted access to the External Credential Principal.

1. Open the target **Profile** or **Permission Set**
2. Find **Enabled External Credential Principal Access**
3. Add the Principal created in Step 2.
