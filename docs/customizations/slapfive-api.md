---
description: >-
  SlapFive has a powerful Application Programming Interface (API) that includes
  webhooks, GET and POST endpoints.
---

# SlapFive API

## Authentication

When making requests to any SlapFive API endpoint, you must include **api-authorization** as a key in the HTTP header, with your **API Key** as the value. To find or generate your API Key, go to your Admin menu and click Client Settings, and scroll down to the **API Keys** section, where you can copy and paste the value that appears, or generate a new one.

## Pagination

For using GET endpoints to retrieve more than 1,000 records, SlapFive recommends using pagination to retrieve 1,000 records at a time. To do this, include the limit and the offset parameters as URL parameters like this:

```
?limit=1000&offset=0
```

or in the body of the request, like this:

```
{
  "limit": 1000,
  "offset": 0
}
```

## Created and Last Updated Dates

The SlapFive API GET endpoints all include the Created Date and Last Updated Date for each record in their response output, like this:

```
{
 "createdAt":"2025-03-06T20:27:45.111289+00:00",
 "updatedAt":"2025-03-06T20:43:45.122277+00:00"
}
```

## Get Records based on Last Updated Dates

You can append GET URLs with these two parameters to get records that have been updated within a certain period:

This gets all records with an updatedAt date since Junuary 1, 2026, or whatever date you insert.

```
...api/api/customers/?since=2026-01-01
```

This gets all records with an updatedAt date within the last 1,000 hours, or whatever hours you insert.

<pre><code><strong>...api/api/customers/?hoursBack=1000
</strong></code></pre>

These parameters are enabled for these objects: Activities, Boards, Companies, Members, Page Views,  Requests, Request Fulfillment Companies/Members, Request Fulfillment Boards, Shares, and Stories.

## Get Specific Fields

You can append GET URLs with the field names of the fields you want returned, rather than return all fields, like this example for pulling Member (customer) fields:

```
...api/api/customers/?fields=fname,lname,title,email
```

You can also specify the names of fields from related objects, like this example for pulling Company information for the Members:

```
...api/api/customers/?fields=fname,lname,title,email,company.name,company.location
```

## Get Data with Role Filters Applied

You can append GET URLs with scope=Role to filter the data returned using the Role Filters for the specified Role. For example, to filter Company data by the filter for the Company entity defined in the Salesforce Role:

```
...api/api/companies?scope=Role:Salesforce%20Company
```

## Available API endpoints

***

### Boards

#### Get all Boards

This API returns all Boards in an array, with the Board Name and Board ID.

Method: GET\
URL: https://your\_company.slapfive.com/api/api/boards/

#### Get Boards created or changed in last XX hours

This returns Boards that have been created or changed within the specified number of hours.

Method: GET\
URL: https://your\_company.slapfive.com/api/api/boards/?hoursBack=XX

#### Get specific Board and its Stories

This API accepts a Board ID as parameter and returns that Board along with all the Stories on that Board. The Stories are returned with all the data about the Customer who contributed the Story.

Method: GET\
URL: https://your\_company.slapfive.com/api/api/boards/\<boardID>

#### Webhook for new or changed Board

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body:&#x20;

```
{
'webhook_url': the URL that the webhook calls when a Board is created/updated
'webhook_id': 'board'
}
```

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body:&#x20;

```
{
'webhook_url': the URL that was subscribed
}
```

#### Create or update Board

If a Board record exists for the id provided, it updates that record, otherwise it creates a new record. In either case it returns the id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/boards/\
Required: id OR name.\
storyIds: passing storyIds will remove all currently attached Stories from the Board and add the Stories that correspond to the storyIds in the order in which they are provided in the array.\
\
**Sample JSON request data:**

```
{
"id":"cjy4vfgam01eq8357x44uihd3",
"name":"Customer Success Story for IGM",
"templateId":"cjy4vfgam01eo0197xg4uihd3",
"headline":"IGM transforms its customer experience with help from Sandbox",
"tagline":"Success Story",
"body":"This is a sentence or two of text.",
"boardImageUrl":"https://www.anyimageurl.com",
"customUrl":"https://sandbox.slapfive.com/b/435gdfw34/IGM",
"ctaHead":"See Sandbox in Action",
"ctaCopy":"This is a sentence or two of text.",
"ctaLink":"https://sandbox.com/demo",
"ctaLinkText":"Sign up for a demo",
"ctaImageUrl":"https://www.anyimageurl.com",
"tags":"Large, Medium",
"activityTypeOnView_id":"cjy4vfgam01eq8357xg4uihd3",
"howToUse":"This is a sentence or two of text.",
"useAtStages":"Qualification",
"tokenAccessOnly":"true",
"tokenAccessForcedExpirationDays":"2",
"usePreMessage":"true",
"preMessageText":"This is a sentence or two of text.",
"preMessageButtonText":"Agree",
"usePreMessageReceipt":"true",
"dynamicFields": {
      "fieldName1": "value",
      "fieldName2":"value",
      "fieldName3": [                      // replaces PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"dynamicFieldsAdd": {
      "fieldName1": [                      // adds PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"dynamicFieldsDelete": {
      "fieldName1": [                      // deletes PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"customFieldData": [
   "showInSalesforce":"Yes",
   "showInHighSpot":"No"
   ],
"storyIds": [
   "cmjbkaj2x1acw0own4vcoctig",
   "cmj8fbziv09yo0ps66kmzcnbf",
   "cmj8f829u09vj0ospaq0tfasm"
   ]
}
```

**Sample JSON output:**

```
{
"board": {
     "id": "cjy4vfgam01eo0197xg4uihd3"
     }
}
```

#### Delete Board

Delete a Board record by id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/boards/delete

**Sample JSON request data:**

```postman_json
{
  "ids": ["cmoc5omsq6vf345rq1nt4bepe", "cmoc635xn6s600mvag0ehajlp"]
} 
```

***

### Stories

#### Get all Stories

This API returns all Stories, in an array, with all the information from the Story and the Customer who contributed the Story.

Method: GET\
URL: https://your\_company.slapfive.com/api/api/stories/

#### Get Stories created or changed in last XX hours

This API returns Stories that have been created or changed within the specified number of hours.

Method: GET\
URL: https://your\_company.slapfive.com/api/api/stories/?hoursBack=XX

#### Get specific Story

This API accepts a Story ID as parameter and returns that Story with all the data about the Customer who contributed the Story.

Method: GET\
URL: https://your\_company.slapfive.com/api/api/stories/\<storyID>

#### Webhook for new or changed Story

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body:&#x20;

```
{
 'webhook_url': the URL that the webhook calls when a Story is created/updated
 'webhook_id': 'story'
}
```

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body:&#x20;

```
{
 'webhook_url': the URL that was subscribed
}
```

#### Create or update Story

If a Story record exists for the id provided, it updates that record, otherwise it creates a new record. In either case it returns the id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/stories/\
Required for updating a Story:\
&#x20;    id\
Required for creating a new Story: \
&#x20;    customerId OR customerEmail,\
&#x20;    promptId\
&#x20;    type (if media is provided, type will be determined from the media)\
\
**Sample JSON request data:**

```
{
"id":"cjy4vfgam01eq8357xg44ihd3",
"customerId":"cjy4vfgam01eo0197xg4uihd3",
"customerEmail":"customer@company.com",
"promptId":"cjy4vfgam01eo0197xg4uihd3",
"type":"Video",
"url":"https://sandbox.com/asdfsadf",
"label":"What is your favorite thing about Sandbox?",
"text":"See Sandbox in Action",
"summary":"This is sentences of text.",
"transcript":"This is sentences of text.",
"permission":"",
"reviewStatus":"Released",
"source":"Customer inteview",
"sourceUrl":"",
"tags":"Qualification",
"language":"true",
"capturedByUserId":"cjy4vfgam01eo0197xg4uihd3",
"capturedByUserEmail":"user@company.com",
"capturedDate":"2021-10-24",
"nextReviewDate":"2027-06-12 12:00:00",
"dynamicFields": {
      "fieldName1": "value",
      "fieldName2":"value",
      "fieldName3": [                      // replaces PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"dynamicFieldsAdd": {
      "fieldName1": [                      // adds PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"dynamicFieldsDelete": {
      "fieldName1": [                      // deletes PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"media": {
    "url": "https://mediaFileUrl",
    "label": "Media label",
    "transcription": "Transcription text",
    "companyAttachment_id": "cmhdx4r1d00th0os6coae28i5"
    }
}
```

**Sample JSON output:**

```
{
"story": {
     "id": "cjy4vfgam01eo0197xg4uihd3"
     }
}
```

#### Delete Story

Delete a Story record by id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/stories/delete

**Sample JSON request data:**

```postman_json
{
  "ids": ["cmoc5omsq6vf345rq1nt4bepe", "cmoc635xn6s600mvag0ehajlp"]
} 
```

***

### Members

#### Get all Members

Method: GET\
URL: https://your\_company.slapfive.com/api/api/customers/

#### Get Members created or changed in last XX hours

Method: GET\
URL: https://your\_company.slapfive.com/api/api/customers/?hoursBack=XX

#### Get a specific Member by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/customers/\<memberID>

#### Get a specific Member by Email Address

Method: GET\
URL: https://your\_company.slapfive.com/api/api/customers/\<email>

#### Webhook for new or changed Member

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body:&#x20;

```
{
 'webhook_url': the URL that the webhook calls when a Member is created/updated
 'webhook_id': 'member'
}
```

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body:&#x20;

<pre><code>{
<strong> 'webhook_url': the URL that was subscribed
</strong>}
</code></pre>

#### Create or update Member

If a Member record exists with the id, email or salesforceContactId provided, it updates that record, otherwise it creates a new record. In either case it returns the id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/customers/\
Required for updating a Member: id OR email OR salesforceContactId.\
Required for creating new Member: email, fname, lname, companyName.\
Required for updating the Member's salesforceContactId: id, new salesforceContactId.

Logic for associating Member with Company:

* If the companyName and/or companySalesforceAccountId MATCH either of those values for the Company that the Member currently belongs to, keep the Member attached to that Company.
* If the companyName and/or companySalesforceAccountId DO NOT MATCH either of those values for the Company that the Member currently belongs to, but MATCH another Company, associate the Member with that matching Company.
* If the companyName and/or companySalesforceAccountId DO NOT MATCH either of those values for the Company that the Member currently belongs to, and DO NOT MATCH another Company, create a new Company and associate the Member with that new Company.

**Sample JSON request data:**

```
{
"id":"cmhdx4r1w00ti0os6hqs486wv",
"email":"jsmith@abcindustries.com",
"fname":"Joseph",
"lname":"Smith",
"companyName":"ABC Industries",
"phone":"616.765.6787",
"phoneCountryCode":"US",
"title":"VP of Marketing",
"functionalRole":"Marketing",
"avatarImageUrl":"https://www.anyimageurl.com",
"activityTypesWillingToDo": [
      "Speak with an industry analyst", "Take a Reference call", "Network with peers"
   ]
"activityTypesWillingToDoWithLimits": [
      {"name": "Take a Reference Call", "limit": 3},
      {"name": "Case Study", "limit": 1}
   ],
"linkedInUrl":"https://www.linkedin.com/in/josephsmith/",
"twitterHandle":"@joejoesmitty",
"salesforceContactId":"4GH876JhG9765763",
"type":"Client",
"trustedContacts":"joesmith@abc.com, bettyjones@xyz.com",
"activeStatus":"Active",
"inviteStatus":"Member",
"engagementNote":"This text is added to the bottom of the Engagement Note field",
"engagementNoteReplace":"This text replaces what is in the engagementNote field.",
"nominatedBy":"Fred Johnson",
"nominatedDate":"",
"dynamicFields": {
      "fieldName1": "value",
      "fieldName2":"value",
      "fieldName3": [                      // replaces PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"dynamicFieldsAdd": {
      "fieldName1": [                      // adds PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"dynamicFieldsDelete": {
      "fieldName1": [                      // deletes PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"attachments": [
    { 
       "url": "https://mysite.com/filename.pdf",
       "label": "Agreement"
    }
  ],
"companyActiveStatus":"Active",
"companyProgramStatus":"Member",
"companyDescription":"Global Manufacturing company",
"companyLogoUrl":"https://www.anyimageurl.com",
"companyPermissions": [
  "These are the permissions that have been explicitely granted",
  "Name Drop"
  ] 
"companyPermissions_denied": [
  "These are the permissions that the company has explicitely denied"
  ] 
"companyPermissions_unknown": [
  "These are the permissions that have not been explicitely granted or denied"
  ] 
"companySize":"100-500 employees",
"companyIndustry":"Computer Software",
"companyLocation":"Boston, MA",
"companySince":"July 2016",
"companyProductsOwned":"Product A, Product B, Product C",
"companyCompetitorsReplaced":"Competitor X",
"companyBusinessGoals":"World Domination and hyper-growth",
"companyEngagementNotes": "This text is added to the bottom of the Engagement Notes field",
"companyEngagementNotesReplace": "This text replaces what is in the Engagement Notes field",
"companySalesforceAccountId":"4GH876JhG9765763",
"companyTrustedContacts":"joesmith@abc.com, bettyjones@xyz.com",
"companyDynamicFields": {
      "fieldName1": "value",
      "fieldName2":"value",
      "fieldName3": [                      // PICKMANY dynamic fields
           "Value1",
           "Value2"
       ]
    }
}
```

**Sample JSON output:**

```
{
"customer": {
     "id": "cjy4vfgam01eo0197xg4uihd3"
     }
}
```

#### Create or update Members in Bulk

Use the same input fields and rules, but pass multiple objects within an array. The maximum body array size is 1000.

#### Delete Member

Delete a Member record by id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/customers/delete

**Sample JSON request data:**

```postman_json
{
  "ids": ["cmoc5omsq6vf345rq1nt4bepe", "cmoc635xn6s600mvag0ehajlp"]
} 
```

***

### Companies

#### Get all Companies

Method: GET\
URL: https://your\_company.slapfive.com/api/api/companies/\
By default, this endpoint gets Companies changed in the last 24 hours. To also get Companies changed more than 24 hours ago, append the URL with /?hoursBack=XX as described in [Get Companies That Have Been Created or Changed in the Last XX Hours](https://www.slapfive.com/api/#getnewchangedcompanies).

#### Get a specific Company by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/companies/\<id>

#### Get Companies created or changed in last XX hours

Method: GET\
URL: https://your\_company.slapfive.com/api/api/companies/?hoursBack=XX

#### Webhook for new or changed Company

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body:&#x20;

```
{
 'webhook_url': the URL that the webhook calls when a Company is created/updated
 'webhook_id': 'company'
}
```

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body:&#x20;

```
{
 'webhook_url': the URL that was subscribed
}
```

#### Create or update Company

If a Company record exists with the name or salesforceAccountId provided, it updates that record, otherwise it creates a new record. In either case it returns the Company ID.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/companies/\
Required for updating a Company: name OR salesforceAccountId\
Required for creating new Member: name\
Required for updating the Company's name: id, new name.\
Required for updating the Company's salesforceAccountId: id, new salesforceAccountId.

**Sample JSON request data:**

```
{
"id":"cmjso15j1001k0osw6jau3a4r",
"name": "ABC Company",
"description": "Large Manufacturing Company",
"logoUrl":"https://www.anyimageurl.com",
"size": "100 employees",
"industry": "Manufacturing",
"location": “Houston, TX",
"since": "1995",
"productsOwned": "Product A",
"competitorsReplaced": "Competitor A",
"businessGoals": "Make more money",
"salesforceAccountId": "456hg45kj64j25332",
"matchingField1": "Texas",
"matchingField2": "",
"matchingField3": "",
"engagementNotes": "This text is added to the bottom of the Engagement Notes field",
"engagementNotesReplace": "This text replaces whatever is in the Engagement Notes field",
"activeStatus": "Active",
"programStatus": "Member",
"trustedContacts": "joesmith@abc.com, bettyjones@xyz.com",
"anonymizedName": "",
"permissions": [
  "These are the permissions that have been explicitely granted",
  "Name Drop"
  ] 
"permissions_denied": [
  "These are the permissions that the company has explicitely denied"
  ] 
"permissions_unknown": [
  "These are the permissions that have not been explicitely granted or denied",
  "Name Drop"
  ] 
"dynamicFields": {
      "fieldName1": "value",
      "fieldName2":"value",
      "fieldName3": [                      // replaces PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"dynamicFieldsAdd": {
      "fieldName1": [                      // adds PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"dynamicFieldsDelete": {
      "fieldName1": [                      // deletes PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"attachments": [
    { 
       "url": "https://mysite.com/filename.pdf",
       "label": "Agreement"
    }
  ]
}
```

**Sample JSON output:**

```
{
"company": {
     "id": "cjy4vfgam01eo0197xg4uihd3"
     }
}
```

#### Create or update Companies in Bulk

Use the same input fields and rules, but pass multiple objects within an array. The maximum body array size is 1000.

#### Delete Company

Delete a Company record by id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/companies/delete

**Sample JSON request data:**

```postman_json
{
  "ids": ["cmoc5omsq6vf345rq1nt4bepe", "cmoc635xn6s600mvag0ehajlp"]
} 
```

***

### Activities

#### Get all Activities

Method: GET\
URL: https://your\_company.slapfive.com/api/api/activityLogs/

#### Get a specific Activity by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/activityLogs/\<id>

#### Get Activities created or changed in last XX hours

Method: GET\
URL: https://your\_company.slapfive.com/api/api/activityLogs/?hoursBack=XX

#### Webhook for new or changed Activity

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body:&#x20;

```
{
 'webhook_url': the URL that the webhook calls when an Activity is created/updated
 'webhook_id': 'activityLog'
}
```

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body:&#x20;

```
{
 'webhook_url': the URL that was subscribed
}
```

#### Create or update Activity

If an Activity record exists for the id provided, it updates that record, otherwise it creates a new record. In either case it returns the id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/activity/\
Required for creating new Activity: email or customerId, activityName, date\
Required for updating Activity: id

**Sample JSON request data:**

```
{
"id":"sd234gsd432353f4v43534",
"customerId":"ckww22x5o00w70hr78mjp2i1s",
"email":"jsmith@abcindustries.com",
"activityName":"Speak at a conference",
"date":"2026-06-12 12:00:00",
"notes":"Spoke on customer panel at ABC Customer Conference",
"customPoints":400,
"points_override_mode":true,
"dynamicFields": {
      "fieldName1": "value",
      "fieldName2":"value",
      "fieldName3": [                      // replaces PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"dynamicFieldsAdd": {
      "fieldName1": [                      // adds PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"dynamicFieldsDelete": {
      "fieldName1": [                      // deletes PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    }
}
```

**Sample JSON output:**

```
{
"status": "ok",
"message": “added activity type ‘Speak at a conference’ to John Smith”
}
```

#### Create or update Activities in Bulk

Use the same input fields and rules, but pass multiple objects within an array. The maximum body array size is 1000.

#### Delete Activity

Delete an Activity record by id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/activity/delete

**Sample JSON request data:**

```postman_json
{
  "ids": ["cmoc5omsq6vf345rq1nt4bepe", "cmoc635xn6s600mvag0ehajlp"]
} 
```

***

### Requests

#### Get Requests updated in last XX hours

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requests/?hoursBack=XX

#### Get Requests fulfilled in last XX hours

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requests/?fulfillmentHoursBack=XX

#### Get a specific Request by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requests/\<id>

#### Webhook for new or changed Request

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body:&#x20;

```
{
'webhook_url': the URL that the webhook calls when a Request is created/updated
'webhook_id': 'request'
}
```

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body:&#x20;

```
{
'webhook_url': the URL that was subscribed
}
```

#### Create or update Request

If a Request record exists for the id provided, it updates that record, otherwise it creates a new record. In either case it returns the id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/requests/\
Required: needDescription, needByDate\
\
**Sample JSON request data:**

```
{
"id": "53k3kj6322k45k3224",
"needDescription": "2 manufacturing customers in EMEA using product X",
"needFor": "Big Company sales opportunity",
"activityType": "Take a reference call",
"needByDate": "2026-04-29",
"requestDate": "2026-04-20",
"dynamicFields": {
      "fieldName1": "value",
      "fieldName2":"value",
      "fieldName3": [                      // replaces PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"dynamicFieldsAdd": {
      "fieldName1": [                      // adds PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"dynamicFieldsDelete": {
      "fieldName1": [                      // deletes PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"requesterEmail": "bill@slapfive.com",
"requesterName": "Bill Salesguy",
"requester_external_id": "48j3j3k54hj3"      // UserID from CRM
"team": "Sales",
"requestStatus": "New",
"fulfillmentDate": "",
"assignedTo": "dana@slapfive.com",
"note": "This is the note field.",
"opportunityId": "456hg45kj64j25332",
"preferredCustomers":"IBM, Cisco",
"archived":false
}
```

**Sample JSON output:**

```
{
"request": {
     "id": "cjy4vfggds534397xg4uihd3",
     "number": "455"
     }
}
```

#### Delete Request

Delete a Request record by id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/requests/delete

**Sample JSON request data:**

```postman_json
{
  "ids": ["cmoc5omsq6vf345rq1nt4bepe", "cmoc635xn6s600mvag0ehajlp"]
} 
```

***

### Fulfillment Members/Companies

#### Get all Fulfillment Members/Companies

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentMembers/

#### Get Fulfillment Members/Companies for a Request

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentMembers/\<requestID>

#### Get Fulfillment Members/Companies created/changed in last XX hours

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentMembers/?hoursBack=XX

#### Get specific Fulfillment Member/Company by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentMembers/\<id>

#### Webhook for new or changed Fulfillment Member/Company

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body:&#x20;

```
{
'webhook_url': the URL that the webhook calls when a Fulfillment Member is created/updated
'webhook_id': 'fulfillmentMember'
}
```

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body:&#x20;

```
{
'webhook_url': the URL that was subscribed
}
```

#### Create or update Fulfillment Member/Company

If a Request Fulfillment Member record exists for the id provided, it updates that record, otherwise it creates a new record. In either case it returns the id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentCustomers/\
Required for creating new Fulfillment Member/Company: \
&#x20;   request\_number or request\_id;\
&#x20;   customer\_email, customer\_id, or customer\_salesforceContactId;\
&#x20;   company\_name, company\_id, or company\_salesforceAccountId;\
Required for updating Fulfillment Member/Company: id

**Sample JSON request data:**

```
{
"id": "53k3kj6322k45k3224",
"request_Number": "223",
"request_Id": "",
"activityType_name": "Take a reference call",
"needByDate”: "2026-04-29",
"customer_id":"5jjfg834kjjsojeruweg",
"customer_email": "fred@bigcompany.com",
"customer_salesforceContactId": "456hg45kj64j25332",
"company_id":"asdf7sd6fs6adf6asf6",
"company_name": "Big Company",
"company_salesforceAccountId": "456hg45kj64j25332",
"assignedTo_email": "dana@slapfive.com",
"statusChange_status": "Asked",
"statusChange_statusChangeDate": "2026-04-29",
"note":"IBM, Cisco",
"dynamicFields": {
      "fieldName1": "value",
      "fieldName2":"value",
      "fieldName3": [                      // replaces PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"dynamicFieldsAdd": {
      "fieldName1": [                      // adds PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    },
"dynamicFieldsDelete": {
      "fieldName1": [                      // deletes PICKMANY dynamic field values
           "Value1",
           "Value2"
       ]
    }
}
```

**Sample JSON output:**

```
{
"requestFulfillmentMember": {
     "id": "cjy4vfggds534397xg4uihd3"
     }
}
```

***

### Fulfillment Boards

#### Get all Fulfillment Boards

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentBoards/

#### Get Fulfillment Boards for a Request

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentBoards/\<requestID>

#### Get Fulfillment Boards created/changed in last XX hours

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentBoards/?hoursBack=XX

#### Get specific Fulfillment Board by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentBoards/\<id>

#### Webhook for new or changed Fulfillment Board

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body:&#x20;

```
{
'webhook_url': the URL that the webhook calls when a Fulfillment Board is created/updated
'webhook_id': 'fulfillmentBoard'
}
```

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body:&#x20;

{\
‘webhook\_url’: the URL that was subscribed\
}

***

### Campaigns

#### Get all Campaigns

Method: GET\
URL: https://your\_company.slapfive.com/api/api/campaigns/

#### Get specific Campaign by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/campaigns/\<id>

#### Webhook for new or changed Campaign

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body:&#x20;

```
{
'webhook_url': the URL that the webhook calls when a Campaign is created/updated
'webhook_id': 'campaign'
}
```

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body:&#x20;

```
{
'webhook_url': the URL that was subscribed
}
```

***

### Campaign Items

#### Get all Campaign Items for a Campaign

Method: GET\
URL: https://your\_company.slapfive.com/api/api/campaigns/\<campaignId>/items

#### Get specific Campaign Item

Method: GET\
URL: https://your\_company.slapfive.com/api/api/campaign-items/\<id>

#### Webhook for new or changed Campaign Item

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body:&#x20;

```
{
'webhook_url': the URL that the webhook calls when a Campaign Item is created/updated
'webhook_id': 'campaignItem'
}
```

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body:&#x20;

```
{
'webhook_url': the URL that was subscribed
}
```

#### Create or update Campaign Item

If a Campaign Item record exists for the id provided, it updates that record, otherwise it creates a new record. In either case it returns the id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/campaigns/\<campaignId>/items/\
Required URL Parameter: campaignId\
Required Body Parameters: the object "entities" with name/value pairs in which the name is the Campaign Column Header.

**Sample JSON request data:**

```
{
    "id": "cmklm6ojn0c5a0oqzctvu3vtg",
    "entities": {
      "Advocate Name": "habington@pepsico.com",
      "Assigned To": "jeff@slapfive.com",
      "Comments": "this is another note"
  }
}
```

***

### Content Shares

#### Get all Content Shares

Method: GET\
URL: https://your\_company.slapfive.com/api/api/shares/

#### Get a specific Content Share by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/shares/\<id>

#### Webhook for new Content Share

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body:&#x20;

```
{
'webhook_url': the URL that the webhook calls when content is shared
'webhook_id': 'share'
}
```

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body:&#x20;

```
{
'webhook_url': the URL that was subscribed
}
```

#### Delete Content Share

Delete a Content Share record by id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/shares/delete

**Sample JSON request data:**

```postman_json
{
  "ids": ["cmoc5omsq6vf345rq1nt4bepe", "cmoc635xn6s600mvag0ehajlp"]
} 
```

***

### Content Views

#### Get all Content Views

Method: GET\
URL: https://your\_company.slapfive.com/api/api/pageViews/

#### Get a specific Content View by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/pageViews/\<id>

#### Webhook for new Content View

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body:&#x20;

```
{
'webhook_url': the URL that the webhook calls when content is viewed
'webhook_id': 'pageView'
}
```

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body:&#x20;

```
{
'webhook_url': the URL that was subscribed
}
```

#### Delete Content View

Delete a Content View record by id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/pageViews/delete

**Sample JSON request data:**

```postman_json
{
  "ids": ["cmoc5omsq6vf345rq1nt4bepe", "cmoc635xn6s600mvag0ehajlp"]
} 
```

***

### Surveys & Prompts

#### Get a Survey and its Responses by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/sentSurvey/\<id>

#### Get a Survey's Responses by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/sentSurvey/\<id>/responses

#### Get all Prompts

Method: GET\
URL: https://your\_company.slapfive.com/api/api/prompts/

#### Get a specific Prompt by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/prompts/\<id>

#### Send a Prompt

Method: POST\
URL: https://your\_company.slapfive.com/api/api/sendPrompt

Required parameters: customerId, promptId or promptGroupId\
Optional parameters: customGreeting, customSubject

#### Delete Prompt

Delete a Prompt record by id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/prompts/delete

**Sample JSON request data:**

```postman_json
{
  "ids": ["cmoc5omsq6vf345rq1nt4bepe", "cmoc635xn6s600mvag0ehajlp"]
} 
```

#### Webhook for Survey/Prompt Sent/Responded to

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body:&#x20;

```
{
'webhook_url': the URL that the webhook calls when a Survey/Prompt is sent/responded to
'webhook_id': 'promptInvitation'
}
```

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body:&#x20;

```
{
'webhook_url': the URL that was subscribed
}
```

#### Get all Sent Prompts and Responses

Method: GET\
URL: https://your\_company.slapfive.com/api/api/sent-prompts/

#### Get a specific Sent Prompt and Response by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/sent-prompts/\<id>

#### Get a specific Sent Survey and Response with each Sent Prompt and Response from the Survey by ID

\<id> = response\_group\_id

Method: GET\
URL: https://your\_company.slapfive.com/api/api/sent-prompts/\<id>

***

### Opportunities

#### Get all Opportunities

Method: GET\
URL: https://your\_company.slapfive.com/api/api/opportunities/

#### Get a specific Opportunity by internal ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/opportunities/\<id>

#### Get a specific Opportunity by CRM opportunity ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/opportunities/\<opportunity\_id>

#### Create or update Opportunity

If an Opportunity record exists for the id or opportunity\_id provided, it updates that record, otherwise it creates a new record. In either case it returns the id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/opportunities/\
\
**Sample JSON request data:**

```
{
    "id":"c54g9dfgjlksgdfjlksdfgjsd",
    "opportunity_id": "123456789",
    "name": "Frisco Software - Enterprise License 2",
    "description": "This is the description",
    "url": "https://frisco.salesforce.com/opportunity/123456789",
    "stage": "Qualification",
    "amount": 100000,
    "is_closed": false,
    "is_won": false,
    "close_date": null,
    "crm_type": "salesforce",
    "external_account_id": null,
    "type": "New Business",
    "lead_source": "Customer Referral",
    "externalContacts": []
}
```

**Sample JSON output:**

```
{
"opportunity": {
     "id": "cjy4vfggds534397xg4uihd3"
     }
}
```

### Client Settings

#### Get Client Settings

Use this endpoint to retrieve Activity Types & Scores, Dynamic Fields, and other Client Settings.

Method: GET\
URL: https://your\_company.slapfive.com/api/api/client

#### Create or Update Activity Types

If an Activity Type record exists for the id provided, it updates that record, otherwise it creates a new record.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/activity-types/\
Required: \
&#x20;   name OR id\
\
**Sample JSON request data:**

```
[
   {
      "id": "cmjx1gxlz0guv0oqz5zj4ghyh",
      "name": "Take a Reference Call",
      "activityCategory": "Advocacy",
      "activityCategory_id": "id",
      "points": 100;
      "includeOnRequestForm": true,
      "allowBonusOptions": false,
      "parent": "Reference Activities",
      "parent_id": "id"
   }
]
```

**Sample JSON output:**

```
[
   {
       "id": "cmjx1gxlz0guv0oqz5zjmghyh",
       "name": "Case Study Interview",
       "points": 100,
       "includeOnRequestForm": true,
       "allowBonusOptions": false,
       "parent_id": null,
       "activityCategory_id": null,
       "__typename": "ActivityType",
       "success": "inserted"
   }
]
```

#### Create or Update Dynamic Field Picklist Values

If a Picklist value record exists for the id provided, it updates that record, otherwise it creates a new record.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/dynamic-fields/**:fieldId**/picklist-values/\
To get the :fieldId, use the [Get Client Settings](https://docs.slapfive.com/customizations/slapfive-api#get-client-settings) endpoint.\
Required: \
&#x20;   name OR id\
\
**Sample JSON request data:**

```
[
   {
      "id": "cmjx360k90hh60ps14ebm31fw",
      "name": "Value 1",
      "order": 10
   },
   {
      "name": "Value 2",
      "order": 12
   }
]
```

**Sample JSON output:**

```
[
   {
      "id": "cmjx360k90hh60ps14ebm31fw",
      "name": "Value 1",
      "order": 10,
      "dynamic_field_id": "cleolm2ye000d3bahwyf3klm0",
      "__typename": "DynamicFieldPickListValue",
      "success": "inserted",
      "index": 0
   },
   {
      "id": "cmjx360k70hh50ps17f490xmw",
      "name": "Value 2",
      "order": 12,
      "dynamic_field_id": "cleolm2ye000d3bahwyf3klm0",
      "__typename": "DynamicFieldPickListValue",
      "success": "inserted",
      "index": 1
   }
]
```

### Prompt the SlapFive AI Assistant

Prompt the AI Assistant and get a response.

Method: POST\
URL: https://your\_company.slapfive.com/api/ai/assistant/\
Required: \
&#x20;   message\
\
**Sample JSON request data:**

```
{
      "message": "Your AI Assistant Prompt",      
}
```

\
**Sample JSON output:**

```
{
       "text": "This is the response to the AI Assistant Prompt",
       "usage": {}
}
```
