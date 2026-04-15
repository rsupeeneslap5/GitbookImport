---
description: >-
  SlapFive uses Workato as its integration and workflow automation platform to
  securely connect with customer systems (e.g., CRM, marketing automation,
  customer success platforms).
---

# How SlapFive uses Workato

Workato enables SlapFive to automate data flows and business processes without requiring custom-built integrations.

***

### What Workato Does in SlapFive

Workato acts as an **orchestration layer** between SlapFive and external systems.

Typical use cases include:

* Syncing customer and contact data (e.g., from Salesforce, HubSpot)
* Triggering workflows based on customer activity
* Sending or receiving data via APIs or webhooks
* Automating processes like customer nominations, advocacy actions, and reporting updates

Workato does **not function as a system of record**.

***

### Data Handling Model

* **In transit:** Data is securely transmitted between systems via encrypted API calls
* **Processing:** Workato processes data in real-time to execute workflows
* **At rest:** Minimal data is stored, limited to:
  * Job execution logs
  * Metadata required for workflow operation

SlapFive configures workflows to **minimize data persistence** within Workato wherever possible.

***

### Types of Data Processed

Depending on the customer’s configuration, Workato may process:

* Contact data (e.g., name, email, company)
* Customer account data
* Activity or engagement data
* Workflow-related metadata

Sensitive data (e.g., financial, health, or highly regulated data) is **not required** for standard SlapFive use cases.

***

### Security & Compliance

Workato maintains industry-standard security controls, including:

* SOC 2 Type II compliance
* Encryption in transit (TLS 1.2+)
* Encryption at rest (AES-256)
* Role-based access controls (RBAC)
* Audit logging and monitoring

SlapFive enforces least-privilege access and secure credential management when configuring integrations.

***

### Data Flow Architecture (High-Level)

1. External system (e.g., CRM) triggers an event or API call
2. Workato receives and processes the event
3. Workato executes workflow logic (transform, route, trigger actions)
4. Data is sent to SlapFive and/or other connected systems

Workato acts only as a **transient processor**, not a destination for long-term storage.

***

### Subprocessor Role

Workato is a **subprocessor** in the SlapFive architecture.

* It processes data solely to execute customer-configured workflows
* It does not independently use or analyze customer data
* Its access is limited to the scope required for integration tasks

Workato is included in SlapFive’s official subprocessor list and governed under applicable Data Processing Agreements (DPAs).

***

### Customer Control & Configuration

* Integrations are configured per customer requirements
* Customers control which systems are connected and what data is shared
* Workflows can be customized to limit or exclude specific data fields

***

### Summary

* Workato enables secure, scalable integrations without custom code
* It operates as a real-time workflow engine, not a data store
* Data exposure is minimized and controlled by design
* It meets enterprise security and compliance standards
