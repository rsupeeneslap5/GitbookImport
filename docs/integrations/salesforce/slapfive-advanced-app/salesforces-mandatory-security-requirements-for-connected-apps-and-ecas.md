---
description: >-
  Salesforce's Mandatory Security Updates for Connected Apps and ECAs do not
  apply to the SlapFive Advanced App, this section explains why
---

# Salesforce's Mandatory Security Updates for Connected Apps and ECAs

On March 18, 2026, Salesforce issued new [Mandatory Security Updates for Connected Apps and ECAs](https://partners.salesforce.com/pdx/s/pcnews/mandatory-security-updates-for-connected-apps-and-ecas-MCFBLDLDQ2TVDZFA22GLAMBVEZGY?language=en_US) that **must be implemented** by Partners enrolled in the AppExchange program in their Partner Applications for any CAs/ECAs that are included or used in connection with a Partner Application, provided or created by the Partner, and in use by more than 2+ customer production orgs by **May 11, 2026**.

SlapFive's engineering team has reviewed these requirements and determined that they don't apply to the SlapFive Advanced App, because the app does not include, distribute, or rely on any SlapFive-owned OAuth Connected App or External Client App. All four controls are configuration settings that exist only on OAuth-enabled Connected Apps/ECAs — that is, apps that obtain Salesforce-issued OAuth access and refresh tokens. The Advanced App's architecture doesn't use that pattern anywhere

#### Proof Key for Code Exchange (PKCE) enabled on Partner-owned CAs/ECAs

The managed package contains no Connected App or External Client App components. We verified this against both our package source and our packaging org.&#x20;

#### Refresh Token Rotation enabled and implemented in application code

No Salesforce OAuth tokens are issued to or handled by the app, so refresh token rotation, idle TTL, and IP allow listing have no surface to apply to. All communication initiated by the app flows outward from your Salesforce org to the SlapFive API over HTTPS, authenticated with a scoped API key managed through Salesforce Named/External Credentials.&#x20;

#### Refresh Token 30-Day Idle Timeout

The SlapFive Connected App contains no OAuth configuration, so PKCE and refresh-token settings do not exist for it. It is used solely for SAML single sign-on (Salesforce acting as identity provider for SlapFive login). SAML flows don't use authorization codes or refresh tokens.

#### Allowlist Ranges for Refresh Tokens

Since there are no Refresh Tokens, Allowlist Ranges don't apply.
