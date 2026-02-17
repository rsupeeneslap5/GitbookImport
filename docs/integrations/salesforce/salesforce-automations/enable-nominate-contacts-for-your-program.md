---
description: >-
  Enable a Salesforce user to nominate a Contact by clicking a button on the
  Contact screen and entering  a short justification. This creates/updates a
  SlapFive Member and adds to Nomination Campaign.
---

# Enable nominate Contacts for your program

## Architecture (at a glance)

* **Screen Flow** → captures user input
* **Custom Object** → stores the nomination
* **Outbound Message** → sends data to integration server
* **Integration Server Recipe** → processes the nomination

## How to set it up

Determine the Contact and Account fields that you want to send to SlapFive with the nomination. The required Contact fields are First Name, Last Name, Email, and Account Name. You may also want to send the Contact's Title, location or address, and any other fields from the Contact or its Account that can help you engage that customer as a Member in SlapFive.

### Step 1: Create the Custom Object (one-time setup)

Go to **Setup → Objects and Fields → Object Manager** and click **Create →Custom Object.**

**Object Name:** `SlapFive Nomination`\
**API Name:** `SlapFive_Nomination__c`

Create the following fields and save the object:

1. **Contact**
   * Type: Lookup (Contact)
   * API Name: `Contact__c`
   * Required: Yes
2. **Nomination Reason**
   * Type: Long Text Area (32,768)
   * API Name: `Nomination_Reason__c`
   * Required: Yes
3. **Submitted By**
   * Type: Lookup (User)
   * API Name: `Submitted_By__c`
   * Required: Optional but recommended
4. **Status**
   * Type: Picklist
   * API Name: `Status__c`
   * Values:
     * Submitted
     * Processed
     * Error
   * Default Value: `Submitted`

### Step 2: Create the Outbound Message

Go to **Setup → Outbound Messages → New Outbound Message.**

* **Object:** SlapFive Nomination
* **Endpoint URL:** _Provided by SlapFive_
* **User to Send As:** Automated Process

Select **Fields to Send**:

* Record Id
* Contact\_\_c
* Nomination\_Reason\_\_c
* Submitted\_By\_\_c
* Status\_\_c
* CreatedDate

Save and **Activate** the Outbound Message.

### Step 3: Create the Screen Flow

Go to **Setup → Flows → New Flow → Screen Flow,** create the variable and add these elements, then Save and **Activate** the Flow.&#x20;

#### Create a Variable to receive the Contact Id automatically:

* **API Name:** `recordId`
* **Data Type:** Text
* **Available for Input:** ✅

#### Add a _**Screen**_ element:

* **Long Text Area**
  * Label: The question you want to ask, such as _Why are you nominating this contact?_
  * API Name: `nominationReason`
  * Required: ✅

#### Add a _Create Records_ element

* **Label:** `Create SlapFive Nomination`
* **API Name:** `Create_SlapFive_Nomination`
* **How many records to create:** select One
* **How to set record field values:** select Manually
* **Object:** SlapFive\_Nomination\_\_c
* **Set Field Values:** Map the fields like this:
  * Contact\_\_c = `{!recordId}`
  * Nomination\_Reason\_\_c = `{!nominationReason}`
  * Submitted\_By\_\_c = `{!$User.Id}`
  * Status\_\_c = `Submitted`

This record creation triggers the Outbound Message automatically.

#### (Optional) Confirmation Screen

Add a final Screen:

* Message: _Nomination submitted successfully._

### Step 4: Add the Flow to the Contact Page

Go to **Object Manager → Contact → Page Layouts**

1. Open the desired page layout.
2. In **Salesforce Mobile and Lightning Experience Actions**, drag **Flow.**
3. Select the Flow you just created.
4. Save

### Step 5: Submit a test nomination

Go to a Contact record, click the new Nomination button, and let your SlapFive Coach know so we can do the final configurations and activate the automation.
