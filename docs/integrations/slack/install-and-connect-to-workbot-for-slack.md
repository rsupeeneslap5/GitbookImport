---
description: >-
  This section covers how to install and establish your Workbot for Slack
  Connection within SlapFive's Embedded Integration.
---

# Install and Connect to Workbot for Slack

Workbot is a Slack app that SlapFive uses to run automated workflows and notifications directly inside your Slack workspace. Setup involves three stages: configuring a Slash Command in Slack, connecting Workbot within SlapFive, and inviting Workbot to the relevant channels. The Slash Command setup must be completed once per Slack workspace by an admin.

### Step 1: Install the Workbot for Slack App

If you have never used Workbot in your Slack environment, you must install it first. Otherwise skip this step and go to Step 2.

In Slack, click **Apps** in the left sidebar, then select **Add apps**, or go directly to the Slack App Directory in your browser.

* [ ] **Search for “Workbot” and** look for **Workbot by Workato**.
* [ ] Select the Workbot app and click **Add to Slack**.
* [ ] Slack will display the permissions Workbot requires (for example, posting messages, responding to interactions). Click **Allow** to approve the installation.
* [ ] Once approved, Workbot will be installed in your Slack workspace and available to all users.

### Step 2: Set Up the Slash Command in Your Slack Workspace

Open the following URL in your browser: [https://your-workspace.slack.com/apps/A0F82E8CA-slash-commands](https://your-workspace.slack.com/apps/A0F82E8CA-slash-commands)

* [ ] On the Slash Command App page, click **Add to Slack.**
* [ ] On the next screen, define the command you want to use. We recommend `/reference`, though `/startrequest` or `/ref` are also common options.
* [ ] Click **Add Slash Command Integration.**
* [ ] On the following screen, scroll to the **Integration Settings** section and paste the Webhook URL provided by the SlapFive team.
* [ ] Locate and copy the **Verification Token** displayed on this screen — you will need it in Step 3.
* [ ] Scroll to the bottom of the page and click **Save Integration.**

### Step 3: Connect to Workbot for Slack App

In SlapFive, go to your **Client Settings > Integrations** and click on **Workbot for Slack Connection**.

* [ ] Under **Advanced**, click **Show** to expand the section.
* [ ] In the **Slash commands verification tokens** field, paste the Token you copied in the previous step.
* [ ] Click the **Connect** button.

### Step 4: Invite Workbot to your Slack Channel

If you're using SlapFive's reference request and approval automation, you'll need to invite Workbot to the Slack channel where users will submit reference requests, see approval notifications, and respond to messages. This can be an existing channel or a new one you create for this purpose.

To invite Workbot, run the following command in that channel:

&#x20;         /invite @Workbot
