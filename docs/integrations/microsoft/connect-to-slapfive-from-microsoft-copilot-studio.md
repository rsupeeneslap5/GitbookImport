---
description: >-
  This section covers how to establish your connection to SlapFive's MCP Server
  from Copilot.
---

# Connect to SlapFive from Microsoft Copilot Studio

Connect Microsoft Copilot Studio to SlapFive's MCP Server so authorized users can access your SlapFive data. The connection uses Streamable HTTP.

Recommended setup: Use the Copilot Studio MCP onboarding wizard. A Power Apps custom connector is an alternative for advanced networking or data-loss-prevention (DLP) requirements.

### Before you begin

* You need SlapFive tenant administrator access to configure the MCP connector and a Copilot Studio account with permission to add tools to an agent.
* Choose an authentication approach: organization-wide API key or per-user OAuth 2.0. Your SlapFive MCP mode must match your Copilot Studio selection.
* For OAuth, coordinate with your SlapFive team to register the connector redirect URL before completing authorization.

### Authentication methods

| SlapFive setting            | Copilot Studio selection | Access model                                                         |
| --------------------------- | ------------------------ | -------------------------------------------------------------------- |
| Organization-wide (API key) | API key                  | A shared credential uses the organization role selected in SlapFive. |
| Per-user login (OAuth)      | OAuth 2.0                | Users authenticate through the tenant’s login flow.                  |

Security note: API keys work only when organization-wide API key mode is enabled. Select an appropriate organization role and grant access only to the tools your agent needs.

### MCP server URLs

| Environment                     | URL                               |
| ------------------------------- | --------------------------------- |
| Production                      | https://app.slapfive.com/mcp      |
| Stage (testing)                 | https://stage.slapfive.com/mcp    |
| Tenant-specific (use for OAuth) | https://{tenant}.slapfive.com/mcp |

Replace {tenant} with your SlapFive tenant subdomain. Use the tenant-specific URL for OAuth so authorization is directed to the correct tenant.

### Option A: Connect with an API key (simplest)

1\. Configure SlapFive

* [ ] In SlapFive, open Settings → Integrations / AI settings → MCP connector.
* [ ] Select Organization-wide (API key), choose the organization role that should govern access, and save.
* [ ] Select Generate API key. Copy the key and store it securely. If a key already exists, use Reveal API key to retrieve it.

Only one API key is valid per tenant. Generating a new key invalidates the previous key; deleting it revokes access.

2\. Add the server in Copilot Studio

* [ ] Open your agent and select Tools → Add a tool → New tool → Model Context Protocol.
* [ ] Enter these values.

| Field              | Value                                                                                      |
| ------------------ | ------------------------------------------------------------------------------------------ |
| Server name        | SlapFive                                                                                   |
| Server description | Query SlapFive customer information, including members, companies, stories, and campaigns. |
| Server URL         | https://app.slapfive.com/mcp                                                               |
| Authentication     | API key                                                                                    |

* [ ] Enter the server details below, then select API key for authentication and paste your SlapFive key.Select Create, review the tools discovered from SlapFive, and add the server to your agent.

3\. Confirm the connection

* [ ] Open the agent’s test experience and try a relevant read-only request, such as asking it to find customer stories.
* [ ] Confirm the agent can discover and use the intended SlapFive tools. Review any write-action confirmations before approving changes.

### Option B: Connect with per-user OAuth 2.0

Use this approach when individual users should sign in to SlapFive. OAuth setup requires coordination because Copilot Studio uses a fixed connector redirect URL.

1. In SlapFive, open the MCP connector settings, select Per-user login (OAuth), and save.
2. Begin creating the MCP connection or custom connector in Copilot Studio / Power Apps. Find and copy the exact redirect URL shown in the connector’s Security settings.
3. Share that redirect URL with your SlapFive technical contact. They must ensure it is registered in the MCP server’s permitted redirect URLs and in the tenant’s Auth0 application callback URLs. This step is required before sign-in will work.
4. Return to the Copilot Studio MCP wizard. Use https://{tenant}.slapfive.com/mcp, select OAuth 2.0, and supply client credentials if requested.
5. Complete the browser sign-in and consent flow, review discovered tools, and add the connection to your agent.

If you do not have access to OAuth application settings, ask your SlapFive contact to coordinate the redirect URL and client configuration with you.

### Important: Select your tools

Copilot Studio supports a maximum of 70 tools per MCP server. SlapFive can expose more tools than this, so select only the tools your agent needs in the SlapFive MCP connector settings before connecting. Keep the selection at 70 or fewer. The SlapFive selection controls which tools the server exposes; your Power Platform DLP policies may also affect access.

| Issue                               | What to check                                                                                                                                             |
| ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| No tools appear or discovery fails  | Confirm the HTTPS URL ends in /mcp. Reduce the selected tools to 70 or fewer in SlapFive, then reconnect.                                                 |
| API key is rejected / invalid token | Confirm Organization-wide (API key) is enabled and the current key was entered. A regenerated key invalidates the old one.                                |
| OAuth redirect mismatch             | Confirm the exact connector redirect URL has been registered by the SlapFive team in both required locations; even small differences can prevent sign-in. |
| OAuth login fails                   | Confirm you are using your tenant-specific hostname and can sign in to the correct SlapFive tenant.                                                       |
| Tools return no results             | Check the selected SlapFive tools and the permissions associated with the configured organization role or signed-in user.                                 |
| Connection blocked by policy        | Ask your Power Platform administrator to review applicable DLP and connector policies.                                                                    |

