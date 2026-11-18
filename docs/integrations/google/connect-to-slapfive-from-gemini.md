---
description: >-
  This section covers how to establish your connection to SlapFive's MCP Server
  from Google Gemini.
---

# Connect to SlapFive from Gemini

Connect Google Gemini CLI to SlapFive's MCP Server so authorized users can access your SlapFive data. The connection uses the Model Context Protocol (MCP) over Streamable HTTP.

This guide focuses on Gemini CLI. Other Gemini clients may support MCP but can have different configuration steps.

### Before you begin

* Have administrator access to your SlapFive tenant to configure the MCP connector.
* Install and configure Gemini CLI on the computer where you will use the connection.
* Choose whether the connection should use one organization-wide API key or individual user sign-in.
* For individual sign-in, have your SlapFive tenant subdomain ready.

### Authentication methods

| Method                    | What it means                                                              | When to use                                           |
| ------------------------- | -------------------------------------------------------------------------- | ----------------------------------------------------- |
| Organization-wide API key | One key connects Gemini CLI using the selected SlapFive organization role. | Recommended for Gemini CLI, scripts, and shared bots. |
| Per-user OAuth            | Each user signs in and accesses data under their own permissions.          | For users who should authenticate individually.       |

Important: The authentication method must match the mode saved in SlapFive. API keys work only when Organization-wide (API key) mode is enabled.

**Server addresses**

| Environment                 | MCP endpoint                      |
| --------------------------- | --------------------------------- |
| Production                  | https://app.slapfive.com/mcp      |
| Staging                     | https://stage.slapfive.com/mcp    |
| Tenant-specific (for OAuth) | https://{tenant}.slapfive.com/mcp |

Replace {tenant} with your actual SlapFive tenant subdomain. Use the tenant-specific address for OAuth so sign-in is associated with the correct tenant.

### Option A: Connect with an API key (recommended for Gemini CLI)

**Step 1. Enable API key access in SlapFive**

1. Open SlapFive Settings → Integrations / AI settings → MCP connector.
2. Select Organization-wide (API key).
3. Choose the organization role that should determine the connection’s data access, then save.

**Step 2. Generate and store your API key**

1. In the MCP connector settings, select Generate API key.
2. Copy the key, which begins with mcp\_, and store it securely.

Only one API key is active per tenant. Generating a new key invalidates the previous one. Use Reveal API key to retrieve the current key or Delete to revoke it.

**Step 3. Add the key to your environment**

On the computer running Gemini CLI, store the key in an environment variable instead of placing the actual key in a settings file:

export SLAPFIVE\_MCP\_API\_KEY="mcp\_..."

Replace mcp\_... with your generated key. Make sure the variable is available in the shell session where you launch Gemini CLI.

**Step 4. Configure Gemini CLI**

Edit \~/.gemini/settings.json for your user, or .gemini/settings.json for a project. Add the SlapFive server to the mcpServers configuration:

{\
&#x20; "mcpServers": {\
&#x20;   "slapfive": {\
&#x20;     "httpUrl": "https://app.slapfive.com/mcp",\
&#x20;     "headers": {\
&#x20;       "Authorization": "Bearer $SLAPFIVE\_MCP\_API\_KEY"\
&#x20;     },\
&#x20;     "timeout": 600000,\
&#x20;     "trust": false\
&#x20;   }\
&#x20; }\
}

Use httpUrl (not url): SlapFive uses Streamable HTTP rather than the older SSE connection. Gemini CLI substitutes the environment variable into the Authorization header. Keep trust set to false to retain confirmation prompts for tool calls.

**Step 5. Verify the connection**

Run the following command in your terminal:

gemini mcp list

In Gemini CLI, enter /mcp to view the server status and available tools. You can then try a request such as “List my open content requests” to check whether a SlapFive tool is called.

### Option B: Connect with individual user sign-in (OAuth)

Choose this option if your organization requires each Gemini user to access SlapFive using their own account.

1. In SlapFive Settings → Integrations / AI settings → MCP connector, select Per-user login (OAuth) and save.
2. In your Gemini settings file, configure the tenant-specific SlapFive MCP endpoint using the example below.
3. Launch Gemini CLI and follow the browser sign-in prompt on first use.

{\
&#x20; "mcpServers": {\
&#x20;   "slapfive": {\
&#x20;     "httpUrl": "https://{tenant}.slapfive.com/mcp",\
&#x20;     "oauth": {\
&#x20;       "enabled": true,\
&#x20;       "scopes": \["mcp:tools", "offline\_access"]\
&#x20;     }\
&#x20;   }\
&#x20; }\
}

Replace {tenant} with your SlapFive tenant subdomain. Gemini CLI uses the authorization flow to sign in and manages cached tokens. Access to SlapFive data follows the signed-in user’s permissions.

### Access and security considerations

* API key access uses the organization role selected when the key is configured; it is not tied to an individual SlapFive user.
* Per-user OAuth access uses each signed-in user’s SlapFive permissions.
* Your organization may restrict which SlapFive tools are available through the MCP connector.
* Treat API keys as sensitive credentials. If a key is replaced or revoked, update the environment variable before reconnecting.

### Troubleshooting

**“Authorization required” or a 401 error**

* Confirm that the API key environment variable is set and the Authorization header includes Bearer and the $ variable reference.
* Confirm the MCP connector is set to the authentication mode you are using.
* For OAuth, confirm you are using your tenant-specific URL and can sign in to that tenant.

**“Invalid token”**

The API key may have been regenerated. Use Reveal API key in SlapFive to retrieve the current key, update your environment variable, and reconnect.

**“SSE stream disconnected”**

Check settings.json. Use httpUrl rather than url: the SlapFive MCP endpoint uses Streamable HTTP.

**Tools do not appear or results are empty**

* Ask your SlapFive administrator to confirm which tools are enabled for your tenant.
* For API key connections, confirm that the configured organization role has access to the data you expect.
* Use /mcp in Gemini CLI to check the server status and discovered tools.
