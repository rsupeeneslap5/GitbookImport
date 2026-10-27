---
description: This page shows you how to bring platform audit events into your SIEM.
---

# Audit Log API for SIEM Integration

SlapFive exposes a tenant-scoped Audit Log API so your security team can ingest platform audit events into your SIEM (CrowdStrike, Splunk, Sentinel, Chronicle, Datadog, etc.). Events are available in near real time and are retrieved with a simple pull model: you poll the endpoint with a `since` cursor and we return the newest events first.

### Environments

| Environment     | Base URL                                      |
| --------------- | --------------------------------------------- |
| Production      | `https://<your-subdomain>.slapfive.com`       |
| Sandbox / Stage | `https://<your-subdomain>.stage.slapfive.com` |

Replace `<your-subdomain>` with your SlapFive tenant subdomain (the same one in your app URL, e.g. `acme` for `acme.slapfive.com`).

### Authentication

Every request must include your SlapFive API key in the `api-authorization` header. You can get your API key on the Basic tab of your Client Settings.

```
api-authorization: <your-api-key>
```

The key is tenant-scoped: it can only ever see audit events for your own tenant. Treat it like any other credential — store it in your secrets manager, rotate it on a schedule, and never embed it in client-side code or logs.

### Endpoint

```
GET /api/audit/events
```

#### Query parameters

| Parameter     | Type               | Description                                                                                                               |
| ------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| `since`       | ISO 8601 timestamp | Only return events occurring at or after this time. Use for incremental/delta polling. Defaults to the beginning of time. |
| `hoursBack`   | integer            | Shorthand for `since = now - N hours`. When provided it overrides `since`.                                                |
| `limit`       | integer            | Max events per request (default 1000).                                                                                    |
| `offset`      | integer            | Pagination offset into the result set.                                                                                    |
| `action`      | string             | Filter to a single action type (see below).                                                                               |
| `entity_type` | string             | Filter to a single entity type (e.g. `Customer`, `Story`).                                                                |
| `fields`      | CSV                | Return only the listed fields, e.g. `fields=id,action,occurred_at`.                                                       |

Events are returned newest-first (`occurred_at` descending).

#### Examples

Fetch everything from the last hour:

```bash
curl -s "https://acme.slapfive.com/api/audit/events?hoursBack=1" \
  -H "api-authorization: $SLAPFIVE_API_KEY"
```

Incremental poll using a stored cursor (recommended for pipelines):

```bash
curl -s "https://acme.slapfive.com/api/audit/events?since=2026-10-27T00:00:00Z&limit=500" \
  -H "api-authorization: $SLAPFIVE_API_KEY"
```

Page through a large window:

```bash
curl -s "https://acme.slapfive.com/api/audit/events?since=2026-10-01T00:00:00Z&limit=1000&offset=1000" \
  -H "api-authorization: $SLAPFIVE_API_KEY"
```

### Response format

The response is a JSON array of audit events:

```json
[
  {
    "id": "cmlabc123",
    "client_id": "<your tenant id>",
    "actor_user_id": "cm4user456",
    "action": "login",
    "target_table": "User",
    "target_record_id": "cm4user456",
    "entity_type": "User",
    "occurred_at": "2026-10-27T14:02:11.481Z",
    "ip_address": "203.0.113.10",
    "user_agent": "Mozilla/5.0 ...",
    "details": { "actor": { "id": "...", "name": "Jane Doe", "email": "jane@acme.com" } },
    "source": "api-server",
    "severity": "info",
    "actor": { "id": "cm4user456", "name": "Jane Doe", "email": "jane@acme.com" }
  }
]
```

| Field                          | Meaning                                                     |
| ------------------------------ | ----------------------------------------------------------- |
| `id`                           | Unique event ID (safe dedup key for your pipeline).         |
| `action`                       | What happened (e.g. `login`, `create`, `update`, `delete`). |
| `entity_type` / `target_table` | The object the event relates to.                            |
| `target_record_id`             | The specific record affected, when applicable.              |
| `actor` / `actor_user_id`      | The user (or API key identity) that performed the action.   |
| `occurred_at`                  | Event timestamp (UTC, ISO 8601).                            |
| `source`                       | Which SlapFive subsystem emitted the event.                 |
| `severity`                     | `info` / `warning` / `error` style classification.          |
| `details`                      | Free-form JSON context (diffs, reasons, actor snapshot).    |
| `ip_address`, `user_agent`     | Request metadata for interactive events.                    |

### Ingestion guidance

For a reliable near-real-time pipeline:

1. **Poll on a short interval** — every 1–5 minutes with `hoursBack` slightly larger than your interval (e.g. `hoursBack=2` for a 5-minute job) to absorb clock skew and retries.
2. **Deduplicate on `id`** — overlapping windows mean you may see the same event twice; `id` is stable and unique per event.
3. **Store a high-water mark** — for stricter exactly-once processing, persist the newest `occurred_at` seen and pass it back as `since` on the next poll.
4. **Page when needed** — if a response hits `limit`, follow up with `offset` until a short/empty page comes back.
5. **Backoff on errors** — retry `429`/`5xx` with exponential backoff; audit data is retained server-side so a missed poll is not lost data.

### What events are covered

The audit stream aggregates:

* **Authentication events** — logins (SSO, SAML, username/password), denials.
* **Administrative changes** — role assignments, permission and settings changes.
* **Data mutations** — creates/updates/deletes on tracked platform entities (members, stories, boards, requests, etc.) as emitted by application audit hooks.

Coverage expands over time; if you need a specific event type that you don't see, tell us and we'll confirm whether it's emitted or can be added.

### Security notes

* Keys are tenant-scoped — you cannot see other customers' events.
* Use HTTPS only; the endpoint rejects plain HTTP.
* If you believe a key has leaked, contact us immediately for revocation and rotation.

### Getting access

1. Go to your Client Settings to get your API key for your tenant.
2. Verify access: `curl -i "https://<sub>.slapfive.com/api/audit/events?hoursBack=24&limit=1" -H "api-authorization: <key>"` → expect `200` with a JSON array.
3. Point your ingestion job at the endpoint using the guidance above.
