---
description: >-
  This section covers how to determine the fields to send to Highspot, and the
  source of those fields, including the SlapFive Board and Story fields to map
  to Highspot Items.
---

# Map SlapFive to Highspot

### &#x31;**. Identify Highspot Spots**

You can post SlapFive Boards and Stories to one or more Spots in Highspot. Indicate the Spot Name, the Spot ID, and the rules for which types of Boards and Stories should go into each Spot. The same Board or Story can go into multiple Spots.

<table><thead><tr><th width="170">Spot Name</th><th width="158">Spot ID</th><th>Which types of Boards and Stories go to this Spot?</th></tr></thead><tbody><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>

### **2. Identify Highspot Lists**

You can post SlapFive Boards and Stories to one or more Lists in Highspot. Indicate the List Name, the List ID, and the rules for which types of Boards and Stories should go into each List? The same Board or Story can go into multiple Lists.

<table><thead><tr><th width="170">List Name</th><th width="158">List ID</th><th>Which types of Boards and Stories go to this List?</th></tr></thead><tbody><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>

### **3. Specify field mappings**

This table shows the Highspot fields that get populated, with the associated SlapFive field or value:

<table><thead><tr><th width="207.22555010549974">Highspot Field</th><th width="295.69011128578046">SlapFive field, source or value</th><th align="center">Required?</th></tr></thead><tbody><tr><td>Spot</td><td><em>24-character ID of the Spot</em></td><td align="center">Yes</td></tr><tr><td>Type</td><td><em>web_link</em></td><td align="center">Yes</td></tr><tr><td>URL</td><td>Board URL or Story URL</td><td align="center">Yes</td></tr><tr><td>Title</td><td>Board Name or Story Label</td><td align="center">No</td></tr><tr><td>Description</td><td>Board Headline or Story Summary</td><td align="center">No</td></tr><tr><td>Author</td><td>A person to attribute the content to</td><td align="center">No</td></tr><tr><td>Date Created</td><td>Date of posting to Highspot</td><td align="center">No</td></tr><tr><td>Internal</td><td><em>False</em></td><td align="center">No</td></tr><tr><td>Link Embed Code</td><td>&#x3C;iframe 'SlapFive_URL' frameborder='0'>&#x3C;/iframe></td><td align="center">No</td></tr><tr><td>CMS: ID</td><td>Board ID or Story ID</td><td align="center">No</td></tr><tr><td>CMS: Integration</td><td><em>SlapFive</em></td><td align="center">No</td></tr></tbody></table>

### **4. Flag the Boards and Stories**

You can decide which SlapFive Boards and Stories should post to Highspot. To do this:

1. If you plan to send Boards to Highspot, in SlapFive Settings, create a Dynamic Field for the Board object called _Show in Highspot._ Make it a YES/NO field.
2. If you plan to send Stories to Highspot, repeat step 1 for the Stories object.
3. For all Boards and/or Stories you want to send to Highspot, edit the Board or Story, set the  **Show in Highspot** field to _Yes_, and **Save** the Board or Story.
