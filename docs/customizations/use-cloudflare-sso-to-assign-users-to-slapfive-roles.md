---
description: >-
  If you want to use Cloudflare to provide Single Sign-On access to SlapFive and
  assign each user to a SlapFive Role, you need to do these steps.
---

# Use Cloudflare SSO to assign Users to SlapFive Roles

## Configure Cloudflare Access Policies and SlapFive Roles

To have Cloudflare assign each User to a specific SlapFive Role, you need to set up your SlapFive Roles with names that exactly match each Cloudflare Access Group used for accessing SlapFive.

* [ ] Determine the Cloudflare Access Groups you'll use and make sure each User who you want to have access to SlapFive belongs to one of those Access Groups. If you want dedicated Access Groups for granting SlapFive access, we suggest giving them a prefix like _SlapFive-CSM_.
* [ ] Create each SlapFive Role and assign the appropriate **Entity Access** and **Filters** as described in the [Configure Role-Based Permissions](configure-role-based-permissions.md) section.

