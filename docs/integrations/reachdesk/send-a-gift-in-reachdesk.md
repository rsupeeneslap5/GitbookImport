---
description: This section covers the automation for sending a gift in Reachdesk.
---

# Send a Gift in Reachdesk

For each request to send a gift using Reachdesk, the SlapFive automation engine sends these fields:

<table><thead><tr><th width="292.4444580078125">Field Name</th><th>Explanation</th></tr></thead><tbody><tr><td>Campaign ID *</td><td>The ID of the Reachdesk Campaign that is used to send the gift. If you plan to use different Campaigns for different purposes, provide your SlapFive coach with each Campaign ID and the conditions in which it is used.</td></tr><tr><td>Sender Email *</td><td>Email of the sender — must be an active Reachdesk user</td></tr><tr><td>Recipient Email *</td><td>Email of the gift recipient</td></tr><tr><td>Recipient First Name *</td><td>First name of the gift recipient</td></tr><tr><td>Recipient Last Name *</td><td>Last name of the gift recipient</td></tr><tr><td>Recipient Country Code</td><td>2-letter ISO 3166 code, e.g. US, GB</td></tr><tr><td>Recipient Company Name</td><td>Company of the gift recipient</td></tr><tr><td>Auto-Approve Send?</td><td>true" = auto-process, "false" = pending review, "auto" = try to approve, fall back to pending</td></tr><tr><td>Payment Currency</td><td>3-letter currency code, e.g. USD, GBP. Defaults to campaign currency if omitted.</td></tr><tr><td>Payment Wallet Type</td><td>"User" or "Team". Defaults to User</td></tr><tr><td>Request ID</td><td>Optional unique identifier for idempotency</td></tr></tbody></table>
