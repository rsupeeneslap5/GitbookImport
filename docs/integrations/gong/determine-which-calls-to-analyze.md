---
description: >-
  This section covers how to determine which Gong calls we should analyze for
  discovering signals.
---

# Determine which calls to analyze

By default, the SlapFive automation's **New Call Recording** trigger fires for every call recorded in Gong. Most likely you want to listen to certain calls where your customers are sharing the signals we want, which is most often Customer Success calls. This requires filtering. There is no native "Call Type" field in Gong, so filtering must be done through one of the approaches below.

***

### Option 1: Filter by Workspace (Recommended)

**Best for:** Organizations that have already segmented their Gong instance into separate workspaces per team (e.g., Sales, Customer Success, Support, Recruiting).

Gong allows you to divide your instance into workspaces for distinct teams or use cases. If your Customer Success managers live in their own workspace, you can scope the Automation Rule — and therefore the automation trigger — to one or more workspaces exclusively. The webhook will never fire for calls from other workspaces.

#### Prerequisites

* Your Customer Success team members must be assigned to a dedicated CS workspace in Gong.
* You must be a **Gong Tech Admin** to create or edit Automation Rules.

#### Setup Steps

1. In Gong, go to **Admin Center → Settings → Ecosystem → Automation Rules**.
2. Click **+ Add Rule**.
3. Click the filter icon to open the rule filter dialog.
4. Under the workspace filter, select your **Customer Success workspace**.
5. Click **Save** to apply the filter.
6. In the **Action** field, confirm **Fire webhook** is selected and enter your Workato endpoint URL.
7. Name the rule (e.g., `CS Calls → SlapFive`) and enable it.

> **Why this works:** Gong stores calls in the home workspace of the call owner. By scoping the rule to the CS workspace, only calls owned by CS team members will trigger the webhook — Sales, Support, and Executive calls are excluded automatically.

***

### Option 2: Filter by Team Member or Call Participant (Good)

**Best for:** Organizations that use a single Gong workspace for all teams.

If your teams are not split into separate workspaces, you can filter the Automation Rule by the **call host or participant**. Gong lets you scope the rule to a specific team by selecting a team manager, which automatically includes all members of that manager's team.

#### Prerequisites

* Your Customer Success team must be set up under a CS manager in Gong.
* You must be a **Gong Tech Admin** to create or edit Automation Rules.

#### Setup Steps

1. In Gong, go to **Admin Center → Settings → Ecosystem → Automation Rules**.
2. Click **+ Add Rule**.
3. Click the filter icon to open the rule filter dialog.
4. Under **Call Participants**, search for your CS team manager and select **"Anyone on \[Manager Name]'s team"**.
5. Click **Save** to apply the filter.
6. In the **Action** field, confirm **Fire webhook** is selected and enter your Workato endpoint URL.
7. Name the rule (e.g., `CS Team Calls → SlapFive`) and enable it.

> **Note:** This filter catches any call where a CS team member participated — not just calls they hosted. If you want to restrict to calls where the CS rep was the **host**, select the **Hosted** option in the participant filter.
