---
description: >-
  This page gives things to check if Gmail connections get disconnected when
  used.
---

# Troubleshooting Gmail Connection

If you connect to a Gmail account and the connection is lost the first time SlapFive tries to send an email, it is almost always caused by a security setting in your Google Workspace that blocks or revokes access for third-party apps, not an issue with the accounts themselves.

Have your Google Workspace Admin check the following:

1. Mark Workato as a trusted app.

* [ ] In the Google Admin console (admin.google.com), go to Security > Access and data control > API controls.
* [ ] Click "Manage Third-Party App Access."
* [ ] Find Workato in the list. It should be there because of today's sign-ins. If it isn't, click "Configure new app" and search for Workato.
* [ ] Set its access to "Trusted" and save.

2. Check whether something revoked the access.

* [ ] Go to Reporting > Audit and investigation > OAuth log events.
* [ ] Filter on the two accounts for today. If a "Revoke" event shows up right after the "Grant," the log will show which admin, policy or security app revoked it.

3. Allow Workato in other security tools or policies (if applicable).

* [ ] If you use a SaaS or email security tool that monitors third-party app access, add Workato to its allowlist.
* [ ] If Context-Aware Access is turned on for Gmail (Security > Access and data control > Context-Aware Access), make sure it doesn't block Workato, which connects from its own servers rather than from your network or devices.

Once that's done, reconnect both Gmail connections. If the connection status says Connected, disconnect first, then connect.
