---
description: >-
  The Reference Request Workflow manages the full lifecycle of a customer
  reference request — from the moment a requester selects a Fulfillment Member
  (FM) or company, through approver sign-off
---

# Request Automation Workflow

**Benefits of Automation: Balancing coordination & automation**

1. Automated Matching: Use profile data and rules to identify advocates at scale.
2. Human Coordination: Manually select advocates for high-touch, strategic outreach.
3. Cross-Team Visibility: Ensure sales, marketing, and success teams collaborate efficiently.

<br>

**How It Works — Step by Step**

| 1 | Requester Submits       | The requester selects a specific Fulfillment Member (FM) or a company for their reference request. This triggers the workflow automatically.                                                                                              |
| - | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2 | Approval Email Sent     | An email is sent to the Approver with a form to review the request. If a member was selected, the form shows that member directly. If a company was selected, the Approver sees a list of members from that company and picks who to use. |
| 3 | Approver Reviews        | The approval form also includes an outreach preference: Send (system sends an automated email to the FM) or Not Send (team reaches out personally). The Approver then clicks Approve Request or Reject Request.                           |
| 4 | Approve or Reject       | If rejected, the FM status in SlapFive is updated to Rejected and the flow stops. If approved, the FM status is updated and the next stage begins based on the outreach preference selected.                                              |
| 5 | FM Availability Request | An email is sent to the Fulfillment Member asking for their availability. The FM selects 3 to 5 available timeslots and responds via a form — choosing Accept or Decline.                                                                 |
| 6 | FM Decision             | If the FM declines, their status in SlapFive is updated to Declined and the flow stops. If they accept, the status is updated to Agreed and the workflow moves forward.                                                                   |
| 7 | Requester Notified      | An email is sent to the requester with the FM's details and the timeslots they selected. A form is included for the requester to pick a final confirmed time after coordinating with their prospect.                                      |
| 8 | Scheduled & Confirmed   | Once the requester selects a time, the FM status in SlapFive is updated to Scheduled. The requester receives a confirmation email with the FM's details and the agreed time.                                                              |
| 9 | Post-Call Feedback      | One day after the scheduled call date, an automated feedback email is sent to the FM to capture their experience and the outcome of the reference call.                                                                                   |

**What the Approver Sees — Approval Form Details**

| **Scenario**                  | **What appears in the Approval Form**                                                                              |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Member selected by requester  | The specific FM is displayed directly — Approver reviews and approves or rejects.                                  |
| Company selected by requester | A list of all members from that company is shown — Approver selects which member to use for the reference request. |
| Outreach preference           | Approver also sets: Send (automated email sent to FM) or Not Send (team contacts FM personally).                   |

<br>

**Fulfillment Member Status Flow in SlapFive**

| **Status**         | **What it means**                                                                               |
| ------------------ | ----------------------------------------------------------------------------------------------- |
| Requested          | Request submitted — waiting for Approver to review and decide.                                  |
| Rejected           | Approver rejected the request — flow stops, FM is not contacted.                                |
| Asked              | Approver approved — email sent to FM asking for available timeslots.                            |
| Declined           | FM declined to participate — flow stops, no scheduling takes place.                             |
| Agreed             | FM accepted and provided timeslots — requester notified to coordinate and confirm a final time. |
| Scheduled          | Requester confirmed a time — call is booked, both parties have the confirmed details.           |
| Feedback Requested | One day after the scheduled call, a feedback email is automatically sent to the FM.             |
