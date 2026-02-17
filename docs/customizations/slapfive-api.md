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

&#x20;   ?limit=1000\&offset=0

or in the body of the request, like this:

&#x20;  {\
&#x20;    "limit": 1000,\
&#x20;    "offset": 0\
&#x20;  }

## Created and Last Updated Dates

The SlapFive API GET endpoints all include the Created Date and Last Updated Date for each record in their response output, like this:

{\
&#x20;"createdAt":"2025-03-06T20:27:45.111289+00:00",\
&#x20;"updatedAt":"2025-03-06T20:43:45.122277+00:00"\
}

## Get Records based on Last Updated Dates

You can append GET URLs with these two parameters to get records that have been updated within a certain period:

**?since=2025-01-01** \
This gets all records with an updatedAt date since January 1, 2025, or whatever date you insert.

**?hoursBack=1000**\
This gets all records with an updatedAt date within the last 1,000 hours, or whatever hours you insert.

These parameters are enabled for these objects: Activities, Boards, Companies, Members, Page Views,  Requests, Request Fulfillment Companies/Members, Request Fulfillment Boards, Shares, and Stories.

## Get Specific Fields

You can append GET URLs with the field names of the fields you want returned, rather than return all fields, like this example for pulling Member (customer) fields:

...api/api/customers/?fields=fname,lname,title,email

You can also specify the names of fields from related objects, like this example for pulling Company information for the Members:

...api/api/customers/?fields=fname,lname,title,email,company.name,company.location

## Available API endpoints

### Get all Boards

This API returns all Boards in an array, with the Board Name and Board ID.

Method: GET\
URL: https://your\_company.slapfive.com/api/api/boards/

### Get Boards created or changed in last XX hours

This returns Boards that have been created or changed within the specified number of hours.

Method: GET\
URL: https://your\_company.slapfive.com/api/api/boards/?hoursBack=XX

### Get specific Board and its Stories

This API accepts a Board ID as parameter and returns that Board along with all the Stories on that Board. The Stories are returned with all the data about the Customer who contributed the Story.

Method: GET\
URL: https://your\_company.slapfive.com/api/api/boards/\<boardID>

### Webhook for new or changed Board

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body: {\
‘webhook\_url’: the URL that the webhook calls when a Board is created/updated\
‘webhook\_id’: ‘board’\
}

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body: {\
‘webhook\_url’: the URL that was subscribed\
}

### Create or update Board

If a Board record exists for the id provided, it updates that record, otherwise it creates a new record. In either case it returns the id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/boards/\
Required: id OR name.\
storyIds: passing storyIds will remove all currently attached Stories from the Board and add the Stories that correspond to the storyIds in the order in which they are provided in the array.\
\
**Sample JSON request data:**

{\
"id":"cjy4vfgam01eq8357x44uihd3",\
"name":"Customer Success Story for IGM",\
"templateId":"cjy4vfgam01eo0197xg4uihd3",\
"headline":"IGM transforms its customer experience with help from Sandbox",\
"tagline":"Success Story",\
"body":"This is a sentence or two of text.",\
"boardImageUrl":"https://www.anyimageurl.com",\
"customUrl":"https://sandbox.slapfive.com/b/435gdfw34/IGM",\
"ctaHead":"See Sandbox in Action",\
"ctaCopy":"This is a sentence or two of text.",\
"ctaLink":"https://sandbox.com/demo",\
"ctaLinkText":"Sign up for a demo",\
"ctaImageUrl":"https://www.anyimageurl.com",\
"tags":"Large, Medium",\
"activityTypeOnView\_id":"cjy4vfgam01eq8357xg4uihd3",\
"howToUse":"This is a sentence or two of text.",\
"useAtStages":"Qualification",\
"tokenAccessOnly":"true",\
"tokenAccessForcedExpirationDays":"2",\
"usePreMessage":"true",\
"preMessageText":"This is a sentence or two of text.",\
"preMessageButtonText":"Agree",\
"usePreMessageReceipt":"true",\
"dynamicFields": {\
&#x20;     "fieldName1": "value",\
&#x20;     "fieldName2":"value",\
&#x20;     "fieldName3": \[                      // PICKMANY dynamic fields\
&#x20;          "Value1",\
&#x20;          "Value2"\
&#x20;      ]\
&#x20;   },\
"customFieldData": \[\
&#x20;  "showInSalesforce":"Yes",\
&#x20;  "showInHighSpot":"No"\
&#x20;  ],\
"storyIds": \[\
&#x20;  "cmjbkaj2x1acw0own4vcoctig",\
&#x20;  "cmj8fbziv09yo0ps66kmzcnbf",\
&#x20;  "cmj8f829u09vj0ospaq0tfasm"\
&#x20;  ]\
}

**Sample JSON output:**

{\
"board": {\
&#x20;    "id": "cjy4vfgam01eo0197xg4uihd3"\
&#x20;    }\
}

### Delete Board

Delete a Board record by id.

Method: DELETE\
URL: https://your\_company.slapfive.com/api/api/boards/\<id>

### Get all Stories

This API returns all Stories, in an array, with all the information from the Story and the Customer who contributed the Story.

Method: GET\
URL: https://your\_company.slapfive.com/api/api/stories/

### Get Stories created or changed in last XX hours

This API returns Stories that have been created or changed within the specified number of hours.

Method: GET\
URL: https://your\_company.slapfive.com/api/api/stories/?hoursBack=XX

### Get specific Story

This API accepts a Story ID as parameter and returns that Story with all the data about the Customer who contributed the Story.

Method: GET\
URL: https://your\_company.slapfive.com/api/api/stories/\<storyID>

### Webhook for new or changed Story

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body: {\
‘webhook\_url’: the URL that the webhook calls when a Story is created/updated\
‘webhook\_id’: ‘story’\
}

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body: {\
‘webhook\_url’: the URL that was subscribed\
}

### Create or update Story

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

{\
"id":"cjy4vfgam01eq8357xg44ihd3",\
"customerId":"cjy4vfgam01eo0197xg4uihd3",\
"customerEmail":"customer@company.com",\
"promptId":"cjy4vfgam01eo0197xg4uihd3",\
"type":"Video",\
"url":"https://sandbox.com/asdfsadf",\
"label":"What is your favorite thing about Sandbox?",\
"text":"See Sandbox in Action",\
"summary":"This is sentences of text.",\
"transcript":"This is sentences of text.",\
"permission":"",\
"reviewStatus":"Released",\
"source":"Customer inteview",\
"sourceUrl":"",\
"tags":"Qualification",\
"language":"true",\
"capturedByUserId":"cjy4vfgam01eo0197xg4uihd3",\
"capturedByUserEmail":"user@company.com",\
"capturedDate":"2021-10-24",\
"nextReviewDate":"2027-06-12 12:00:00",\
"dynamicFields": {\
&#x20;     "fieldName1": "value",\
&#x20;     "fieldName2":"value",\
&#x20;     "fieldName3": \[                      // PICKMANY dynamic fields\
&#x20;          "Value1",\
&#x20;          "Value2"\
&#x20;      ]\
&#x20;   },\
"media": {\
&#x20;   "url": "https://mediaFileUrl",\
&#x20;   "label": "Media label",\
&#x20;   "transcription": "Transcription text",\
&#x20;   "companyAttachment\_id": "cmhdx4r1d00th0os6coae28i5"\
&#x20;   }\
}

**Sample JSON output:**

{\
"story": {\
&#x20;    "id": "cjy4vfgam01eo0197xg4uihd3"\
&#x20;    }\
}

### Delete Story

Delete a Story record by id.

Method: DELETE\
URL: https://your\_company.slapfive.com/api/api/stories/\<id>

### Get all Members

Method: GET\
URL: https://your\_company.slapfive.com/api/api/customers/

### Get Members created or changed in last XX hours

Method: GET\
URL: https://your\_company.slapfive.com/api/api/customers/?hoursBack=XX

### Get a specific Member by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/customers/\<memberID>

### Get a specific Member by Email Address

Method: GET\
URL: https://your\_company.slapfive.com/api/api/customers/\<email>

### Webhook for new or changed Member

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body: {\
‘webhook\_url’: the URL that the webhook calls when a Member is created/updated\
‘webhook\_id’: ‘member’\
}

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body: {\
‘webhook\_url’: the URL that was subscribed\
}

### Create or update Member

If a Member record exists with the id, email or salesforceContactId provided, it updates that record, otherwise it creates a new record. In either case it returns the id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/customers/\
Required for updating a Member: id OR email OR salesforceContactId.\
Required for creating new Member: email, fname, lname, companyName.

When updating by id, you can pass a different salesforceContactId to update that field, and pass a different companyName to associate the Member with that Company.

**Sample JSON request data:**

{\
"id":"cmhdx4r1w00ti0os6hqs486wv",\
"email":"jsmith@abcindustries.com",\
"fname":"Joseph",\
"lname":"Smith",\
"companyName":"ABC Industries",\
"phone":"616.765.6787",\
"title":"VP of Marketing",\
"avatarImageUrl":"https://www.anyimageurl.com",\
"activityTypesWillingToDo": \[\
&#x20;     "Speak with an industry analyst", "Take a Reference call", "Network with peers"\
&#x20;  ]\
"activityTypesWillingToDoWithLimits": \[\
&#x20;     {"name": "Take a Reference Call", "limit": 3},\
&#x20;     {"name": "Case Study", "limit": 1}\
&#x20;  ],\
"linkedInUrl":"https://www.linkedin.com/in/josephsmith/",\
"twitterHandle":"@joejoesmitty",\
"salesforceContactId":"4GH876JhG9765763",\
"type":"Client",\
"trustedContacts":"joesmith@abc.com, bettyjones@xyz.com",\
"activeStatus":"Active",\
"inviteStatus":"Member",\
"engagementNote":"This text is added to the bottom of the Engagement Note field",\
"engagementNoteReplace":"This text replaces what is in the engagementNote field.",\
"dynamicFields": {\
&#x20;     "fieldName1": "value",\
&#x20;     "fieldName2":"value",\
&#x20;     "fieldName3": \[                      // PICKMANY dynamic fields\
&#x20;          "Value1",\
&#x20;          "Value2"\
&#x20;      ]\
&#x20;   },\
"attachments": \[\
&#x20;   { \
&#x20;      "url": "https://mysite.com/filename.pdf",\
&#x20;      "label": "Agreement"\
&#x20;   }\
&#x20; ],\
"companyActiveStatus":"Active",\
"companyProgramStatus":"Member",\
"companyDescription":"Global Manufacturing company",\
"companyLogoUrl":"https://www.anyimageurl.com",\
"companyPermissions": \[\
&#x20; "These are the permissions that have been explicitely granted",\
&#x20; "Name Drop"\
&#x20; ] \
"companyPermissions\_denied": \[\
&#x20; "These are the permissions that the company has explicitely denied"\
&#x20; ] \
"companyPermissions\_unknown": \[\
&#x20; "These are the permissions that have not been explicitely granted or denied"\
&#x20; ] \
"companySize":"100-500 employees",\
"companyIndustry":"Computer Software",\
"companyLocation":"Boston, MA",\
"companySince":"July 2016",\
"companyProductsOwned":"Product A, Product B, Product C",\
"companyCompetitorsReplaced":"Competitor X",\
"companyBusinessGoals":"World Domination and hyper-growth",\
"companyEngagementNotes": "This text is added to the bottom of the Engagement Notes field",\
"companyEngagementNotesReplace": "This text replaces what is in the Engagement Notes field",\
"companySalesforceAccountId":"4GH876JhG9765763",\
"companyMatchingField1":"Tier 2",\
"companyMatchingField2":"Manufacturing",\
"companyMatchingField3":"Any value",\
"companyDynamicFields": {\
&#x20;     "fieldName1": "value",\
&#x20;     "fieldName2":"value",\
&#x20;     "fieldName3": \[                      // PICKMANY dynamic fields\
&#x20;          "Value1",\
&#x20;          "Value2"\
&#x20;      ]\
&#x20;   }\
}

**Sample JSON output:**

{\
"customer": {\
&#x20;    "id": "cjy4vfgam01eo0197xg4uihd3"\
&#x20;    }\
}

### Delete Member

Delete a Member record by id.

Method: DELETE\
URL: https://your\_company.slapfive.com/api/api/customers/\<id>

### Get all Companies

Method: GET\
URL: https://your\_company.slapfive.com/api/api/companies/\
By default, this endpoint gets Companies changed in the last 24 hours. To also get Companies changed more than 24 hours ago, append the URL with /?hoursBack=XX as described in [Get Companies That Have Been Created or Changed in the Last XX Hours](https://www.slapfive.com/api/#getnewchangedcompanies).

### Get a specific Company by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/companies/\<id>

### Get Companies created or changed in last XX hours

Method: GET\
URL: https://your\_company.slapfive.com/api/api/companies/?hoursBack=XX

### Webhook for new or changed Company

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body: {\
‘webhook\_url’: the URL that the webhook calls when a Company is created/updated\
‘webhook\_id’: ‘company’\
}

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body: {\
‘webhook\_url’: the URL that was subscribed\
}

### Create or update Company

If a Company record exists with the name or salesforceAccountId provided, it updates that record, otherwise it creates a new record. In either case it returns the Company ID.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/companies/\
Required for updating a Company: name OR salesforceAccountId\
Required for creating new Member: name

**Sample JSON request data:**

{\
"id":"cmjso15j1001k0osw6jau3a4r",\
"name": "ABC Company",\
"description": "Large Manufacturing Company",\
"logoUrl":"https://www.anyimageurl.com",\
"size": "100 employees",\
"industry": "Manufacturing",\
"location": “Houston, TX",\
"since": "1995",\
"productsOwned": "Product A",\
"competitorsReplaced": "Competitor A",\
"businessGoals": "Make more money",\
"salesforceAccountId": "456hg45kj64j25332",\
"matchingField1": "Texas",\
"matchingField2": "",\
"matchingField3": "",\
"engagementNotes": "This text is added to the bottom of the Engagement Notes field",\
"engagementNotesReplace": "This text replaces whatever is in the Engagement Notes field",\
"activeStatus": "Active",\
"programStatus": "Member",\
"trustedContacts": "joesmith@abc.com, bettyjones@xyz.com",\
"anonymizedName": "",\
"permissions": \[\
&#x20; "These are the permissions that have been explicitely granted",\
&#x20; "Name Drop"\
&#x20; ] \
"permissions\_denied": \[\
&#x20; "These are the permissions that the company has explicitely denied"\
&#x20; ] \
"permissions\_unknown": \[\
&#x20; "These are the permissions that have not been explicitely granted or denied",\
&#x20; "Name Drop"\
&#x20; ] \
"dynamicFields": {\
&#x20;     "fieldName1": "value",\
&#x20;     "fieldName2":"value",\
&#x20;     "fieldName3": \[                      // PICKMANY dynamic fields\
&#x20;          "Value1",\
&#x20;          "Value2"\
&#x20;      ]\
&#x20;   },\
"attachments": \[\
&#x20;   { \
&#x20;      "url": "https://mysite.com/filename.pdf",\
&#x20;      "label": "Agreement"\
&#x20;   }\
&#x20; ]\
}

**Sample JSON output:**

{\
"company": {\
&#x20;    "id": "cjy4vfgam01eo0197xg4uihd3"\
&#x20;    }\
}

### Delete Company

Delete a Company record by id.

Method: DELETE\
URL: https://your\_company.slapfive.com/api/api/companies/\<id>

### Get all Activities

Method: GET\
URL: https://your\_company.slapfive.com/api/api/activityLogs/

### Get a specific Activity by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/activityLogs/\<id>

### Get Activities created or changed in last XX hours

Method: GET\
URL: https://your\_company.slapfive.com/api/api/activityLogs/?hoursBack=XX

### Webhook for new or changed Activity

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body: {\
‘webhook\_url’: the URL that the webhook calls when an Activity is created/updated\
‘webhook\_id’: ‘activityLog’\
}

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body: {\
‘webhook\_url’: the URL that was subscribed\
}

### Create or update Activity

If an Activity record exists for the id provided, it updates that record, otherwise it creates a new record. In either case it returns the id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/activity/\
Required for creating new Activity: email or customerId, activityName, date\
Required for updating Activity: id, email

**Sample JSON request data:**

{\
"id":"sd234gsd432353f4v43534",\
"customerId":"ckww22x5o00w70hr78mjp2i1s",\
"email":"jsmith@abcindustries.com",\
"activityName":"Speak at a conference",\
"date":"2026-06-12 12:00:00",\
"notes":"Spoke on customer panel at ABC Customer Conference",\
"customPoints":400,\
"points\_override\_mode":true,\
"dynamicFields": {\
&#x20;     "fieldName1": "value",\
&#x20;     "fieldName2":"value",\
&#x20;     "fieldName3": \[                      // PICKMANY dynamic fields\
&#x20;          "Value1",\
&#x20;          "Value2"\
&#x20;      ]\
&#x20;   }\
}

**Sample JSON output:**

{\
"status": "ok",\
"message": “added activity type ‘Speak at a conference’ to John Smith”\
}

### Delete Activity

Delete an Activity record by id.

Method: DELETE\
URL: https://your\_company.slapfive.com/api/api/activity/\<id>

### Get Requests updated in last XX hours

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requests/?hoursBack=XX

### Get Requests fulfilled in last XX hours

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requests/?fulfillmentHoursBack=XX

### Get a specific Request by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requests/\<id>

### Webhook for new or changed Request

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body: {\
‘webhook\_url’: the URL that the webhook calls when a Request is created/updated\
‘webhook\_id’: ‘request’\
}

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body: {\
‘webhook\_url’: the URL that was subscribed\
}

### Create or update Request

If a Request record exists for the id provided, it updates that record, otherwise it creates a new record. In either case it returns the id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/requests/\
Required: needDescription, needByDate\
\
**Sample JSON request data:**

{\
"id": "53k3kj6322k45k3224",\
"needDescription": "2 manufacturing customers in EMEA using product X",\
"needFor": "Big Company sales opportunity",\
"activityType": "Take a reference call",\
"needByDate": "2026-04-29",\
"requestDate": "2026-04-20",\
"dynamicFields": {\
&#x20;     "fieldName1": "value",\
&#x20;     "fieldName2":"value",\
&#x20;     "fieldName3": \[                      // PICKMANY dynamic fields\
&#x20;          "Value1",\
&#x20;          "Value2"\
&#x20;      ]\
&#x20;   },\
"requesterEmail": "bill@slapfive.com",\
"requesterName": "Bill Salesguy",\
"requester\_external\_id": "48j3j3k54hj3"      // UserID from CRM\
"team": "Sales",\
"requestStatus": "New",\
"fulfillmentDate": "",\
"assignedTo": "dana@slapfive.com",\
"note": "This is the note field.",\
"opportunityId": "456hg45kj64j25332",\
"preferredCustomers":"IBM, Cisco",\
"archived":false\
}

**Sample JSON output:**

{\
"request": {\
&#x20;    "id": "cjy4vfggds534397xg4uihd3",\
&#x20;    "number": "455"\
&#x20;    }\
}

### Delete Request

Delete a Request record by id.

Method: DELETE\
URL: https://your\_company.slapfive.com/api/api/requests/\<id>

### Get all Request Fulfillment Members/Companies

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentMembers/

### Get Request Fulfillment Members/Companies for a Request

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentMembers/\<requestID>

### Get Request Fulfillment Members/Companies created/changed in last XX hours

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentMembers/?hoursBack=XX

### Get specific Request Fulfillment Member/Company by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentMembers/\<id>

### Webhook for new or changed Request Fulfillment Member/Company

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body: {\
‘webhook\_url’: the URL that the webhook calls when a Request Fulfillment Member is created/updated\
‘webhook\_id’: ‘fulfillmentMember’\
}

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body: {\
‘webhook\_url’: the URL that was subscribed\
}

### Create or update Request Fulfillment Member/Company

If a Request Fulfillment Member record exists for the id provided, it updates that record, otherwise it creates a new record. In either case it returns the id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentCustomers/\
Required: \
&#x20;   request\_number or request\_id;\
&#x20;   customer\_email, customer\_id, or customer\_salesforceContactId;\
&#x20;   company\_name, company\_id, or company\_salesforceAccountId;

**Sample JSON request data:**

{\
"id": "53k3kj6322k45k3224",\
"request\_Number": "223",\
"request\_Id": "",\
"activityType\_name": "Take a reference call",\
"needByDate”: "2026-04-29",\
"customer\_id":"5jjfg834kjjsojeruweg",\
"customer\_email": "fred@bigcompany.com",\
"customer\_salesforceContactId": "456hg45kj64j25332",\
"company\_id":"asdf7sd6fs6adf6asf6",\
"company\_name": "Big Company",\
"company\_salesforceAccountId": "456hg45kj64j25332",\
"assignedTo\_email": "dana@slapfive.com",\
"statusChange\_status": "Asked",\
"statusChange\_statusChangeDate": "2026-04-29",\
"note":"IBM, Cisco",\
"dynamicFields": {\
&#x20;     "fieldName1": "value",\
&#x20;     "fieldName2":"value",\
&#x20;     "fieldName3": \[                      // PICKMANY dynamic fields\
&#x20;          "Value1",\
&#x20;          "Value2"\
&#x20;      ]\
&#x20;   }\
}

**Sample JSON output:**

{\
"requestFulfillmentMember": {\
&#x20;    "id": "cjy4vfggds534397xg4uihd3"\
&#x20;    }\
}

### Get all Request Fulfillment Boards

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentBoards/

### Get Request Fulfillment Boards for a Request

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentBoards/\<requestID>

### Get Request Fulfillment Boards created/changed in last XX hours

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentBoards/?hoursBack=XX

### Get specific Request Fulfillment Board by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/requestFulfillmentBoards/\<id>

### Webhook for new or changed Request Fulfillment Board

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body: {\
‘webhook\_url’: the URL that the webhook calls when a Request Fulfillment Board is created/updated\
‘webhook\_id’: ‘fulfillmentBoard’\
}

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body: {\
‘webhook\_url’: the URL that was subscribed\
}

### Get all Campaigns

Method: GET\
URL: https://your\_company.slapfive.com/api/api/campaigns/

### Get specific Campaign by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/campaigns/\<id>

### Webhook for new or changed Campaign

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body: {\
‘webhook\_url’: the URL that the webhook calls when a Campaign is created/updated\
‘webhook\_id’: ‘campaign’\
}

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body: {\
‘webhook\_url’: the URL that was subscribed\
}

### Get all Campaign Items for a Campaign

Method: GET\
URL: https://your\_company.slapfive.com/api/api/campaigns/\<campaignId>/items

### Get specific Campaign Item

Method: GET\
URL: https://your\_company.slapfive.com/api/api/campaign-items/\<id>

### Webhook for new or changed Campaign Item

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body: {\
‘webhook\_url’: the URL that the webhook calls when a Request is created/updated\
‘webhook\_id’: ‘campaignItem’\
}

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body: {\
‘webhook\_url’: the URL that was subscribed\
}

### Create or update Campaign Item

If a Campaign Item record exists for the id provided, it updates that record, otherwise it creates a new record. In either case it returns the id.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/campaigns/\<campaignId>/items/\
Required URL Parameter: campaignId\
Required Body Parameters: the object "entities" with name/value pairs in which the name is the Campaign Column Header.

**Sample JSON request data:**

{\
&#x20;   "id": "cmklm6ojn0c5a0oqzctvu3vtg",\
&#x20;   "entities": {\
&#x20;     "Advocate Name": "habington@pepsico.com",\
&#x20;     "Assigned To": "jeff@slapfive.com",\
&#x20;     "Comments": "this is another note"\
&#x20; }\
}

### Get all Content Shares

Method: GET\
URL: https://your\_company.slapfive.com/api/api/shares/

### Get a specific Content Share by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/shares/\<id>

### Webhook for new Content Share

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body: {\
‘webhook\_url’: the URL that the webhook calls when a Request is created/updated\
‘webhook\_id’: ‘share’\
}

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body: {\
‘webhook\_url’: the URL that was subscribed\
}

### Delete Content Share

Delete a Content Share record by id.

Method: DELETE\
URL: https://your\_company.slapfive.com/api/api/shares/\<id>

### Get all Content Views

Method: GET\
URL: https://your\_company.slapfive.com/api/api/pageViews/

### Get a specific Content View by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/pageViews/\<id>

### Webhook for new Content View

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body: {\
‘webhook\_url’: the URL that the webhook calls when a Request is created/updated\
‘webhook\_id’: ‘pageView’\
}

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body: {\
‘webhook\_url’: the URL that was subscribed\
}

### Delete Content View

Delete a Content View record by id.

Method: DELETE\
URL: https://your\_company.slapfive.com/api/api/pageViews/\<id>

### Get all Prompts

Method: GET\
URL: https://your\_company.slapfive.com/api/api/prompts/

### Get a specific Prompt by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/prompts/\<id>

### Send a Prompt

Method: POST\
URL: https://your\_company.slapfive.com/api/api/sendPrompt

Required parameters: customerId, promptId or promptGroupId\
Optional parameters: customGreeting, customSubject

### Delete Prompt

Delete a Prompt record by id.

Method: DELETE\
URL: https://your\_company.slapfive.com/api/api/prompts/\<id>

### Webhook for new Prompt Response

**Subscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/subscribe

body: {\
‘webhook\_url’: the URL that the webhook calls when a Request is created/updated\
‘webhook\_id’: ‘sentPrompt’\
}

**Unsubscribe:**

Method: POST\
URL: https://slapfive.slapfive.com/api/webhooks/unsubscribe

body: {\
‘webhook\_url’: the URL that was subscribed\
}

### Get all Sent Prompts and Responses

Method: GET\
URL: https://your\_company.slapfive.com/api/api/sent-prompts/

### Get a specific Sent Prompt and Response by ID

Method: GET\
URL: https://your\_company.slapfive.com/api/api/sent-prompts/\<id>

### Get a specific Sent Prompt Group and Response with each Sent Prompt and Response from the Prompt Group by ID

\<id> = response\_group\_id

Method: GET\
URL: https://your\_company.slapfive.com/api/api/sent-prompts/\<id>

### Get Client Settings

Use this endpoint to retrieve Activity Types & Scores, Dynamic Fields, and other Client Settings.

Method: GET\
URL: https://your\_company.slapfive.com/api/api/client

### Prompt the SlapFive AI Assistant

Prompt the AI Assistant and get a response.

Method: POST\
URL: https://your\_company.slapfive.com/api/ai/assistant/\
Required: \
&#x20;   message\
\
**Sample JSON request data:**

\
{\
&#x20;     "message": "Your AI Assistant Prompt",      \
}

\
**Sample JSON output:**

{\
&#x20;      "text": "This is the response to the AI Assistant Prompt",\
&#x20;      "usage": {}\
}

### Create or Update Activity Types

If an Activity Type record exists for the id provided, it updates that record, otherwise it creates a new record.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/activity-types/\
Required: \
&#x20;   name OR id\
\
**Sample JSON request data:**

\[\
&#x20;  {\
&#x20;     "id": "cmjx1gxlz0guv0oqz5zj4ghyh",\
&#x20;     "name": "Take a Reference Call",\
&#x20;     "activityCategory": "Advocacy",\
&#x20;     "activityCategory\_id": "id",\
&#x20;     "points": 100;\
&#x20;     "includeOnRequestForm": true,\
&#x20;     "allowBonusOptions": false,\
&#x20;     "parent": "Reference Activities",\
&#x20;     "parent\_id": "id"\
&#x20;  }\
]

**Sample JSON output:**

\[\
&#x20;  {\
&#x20;      "id": "cmjx1gxlz0guv0oqz5zjmghyh",\
&#x20;      "name": "Case Study Interview",\
&#x20;      "points": 100,\
&#x20;      "includeOnRequestForm": true,\
&#x20;      "allowBonusOptions": false,\
&#x20;      "parent\_id": null,\
&#x20;      "activityCategory\_id": null,\
&#x20;      "\_\_typename": "ActivityType",\
&#x20;      "success": "inserted"\
&#x20;  }\
]

### Create or Update Dynamic Field Picklist Values

If a Picklist value record exists for the id provided, it updates that record, otherwise it creates a new record.

Method: POST\
URL: https://your\_company.slapfive.com/api/api/dynamic-fields/**:fieldId**/picklist-values/\
To get the :fieldId, use the [Get Client Settings](https://docs.slapfive.com/customizations/slapfive-api#get-client-settings) endpoint.\
Required: \
&#x20;   name OR id\
\
**Sample JSON request data:**

\[\
&#x20;  {\
&#x20;     "id": "cmjx360k90hh60ps14ebm31fw",\
&#x20;     "name": "Value 1",\
&#x20;     "order": 10\
&#x20;  },\
&#x20;  {\
&#x20;     "name": "Value 2",\
&#x20;     "order": 12\
&#x20;  }\
]

**Sample JSON output:**

\[\
&#x20;  {\
&#x20;     "id": "cmjx360k90hh60ps14ebm31fw",\
&#x20;     "name": "Value 1",\
&#x20;     "order": 10,\
&#x20;     "dynamic\_field\_id": "cleolm2ye000d3bahwyf3klm0",\
&#x20;     "\_\_typename": "DynamicFieldPickListValue",\
&#x20;     "success": "inserted",\
&#x20;     "index": 0\
&#x20;  },\
&#x20;  {\
&#x20;     "id": "cmjx360k70hh50ps17f490xmw",\
&#x20;     "name": "Value 2",\
&#x20;     "order": 12,\
&#x20;     "dynamic\_field\_id": "cleolm2ye000d3bahwyf3klm0",\
&#x20;     "\_\_typename": "DynamicFieldPickListValue",\
&#x20;     "success": "inserted",\
&#x20;     "index": 1\
&#x20;  }\
]
