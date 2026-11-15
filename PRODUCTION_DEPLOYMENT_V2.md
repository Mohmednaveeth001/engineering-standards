# Enterprise Production Deployment & Operations Standard --- V2.0

> **Purpose:** Controlled release, deployment, cutover, verification,
> operational handover, and recovery for software, automation, APIs, MCP
> servers, AI agents, data pipelines, and infrastructure workloads.\
> **Rule:** A deployment is not complete until the service is verified,
> ownership is accepted, evidence is recorded, and the operational team
> can recover it.

------------------------------------------------------------------------

## Document Control

  -----------------------------------------------------------------------------------------------------
  Field                               Value
  ----------------------------------- -----------------------------------------------------------------
  Project / Service                   `{{PROJECT_NAME}}`

  Release / Build                     `{{VERSION / COMMIT / DIGEST}}`

  Change / Ticket                     `{{CHANGE_ID}}`

  Deployment owner                    `{{OWNER}}`

  Environment / Region                `{{ENVIRONMENT}}`

  Change window                       `{{START – END WITH TIMEZONE}}`

  Deployment strategy                 `{{ROLLING / BLUE-GREEN / CANARY / IN-PLACE / OTHER}}`

  Risk classification                 `{{LOW / MEDIUM / HIGH / CRITICAL}}`

  Status                              `{{PLANNED / APPROVED / IN PROGRESS / COMPLETE / ROLLED BACK}}`

  Related documents                   `{{ARCHITECTURE / RUNBOOK / ROLLBACK / SECURITY}}`
  -----------------------------------------------------------------------------------------------------

## 0. Mandatory Rules

1.  Production changes MUST have an authorized change record and named
    owner.
2.  Deploy only a reviewed, tested, traceable, immutable artifact.
3.  Production secrets MUST be sourced from an approved secret manager
    or platform facility.
4.  Do not run destructive commands without explicit scope,
    authorization, and recovery plan.
5.  Validate backups and recovery feasibility before changes that can
    affect data.
6.  Define objective Go / No-Go and rollback triggers before starting.
7.  Use least-privilege, time-bound deployment access.
8.  Keep a timestamped execution log and evidence for every critical
    step.
9.  If a critical safety, security, data-integrity, or health check
    fails, STOP and follow the decision process.
10. Do not claim success until post-deployment verification and handover
    are complete.

## 1. Release Summary

-   **What is changing:** `{{CHANGE}}`
-   **Why:** `{{REASON}}`
-   **Scope:** `{{SERVICES / TENANTS / REGIONS / DEVICES}}`
-   **User / business impact:** `{{IMPACT}}`
-   **Expected downtime:** `{{NONE / WINDOW}}`
-   **Breaking changes:** `{{DETAILS / NONE}}`
-   **Database / data changes:** `{{DETAILS / NONE}}`
-   **External integrations affected:** `{{DETAILS}}`
-   **Known issues / limitations:** `{{DETAILS}}`

## 2. Release Manifest and Provenance

  ------------------------------------------------------------------------------
  Artifact          Version / immutable      Source / build    Verified
                    identifier               URL               
  ----------------- ------------------------ ----------------- -----------------
  Source commit /   `{{SHA / TAG}}`          `{{URL}}`         \[ \]
  tag                                                          

  Binary / package  `{{VERSION / DIGEST}}`   `{{URL}}`         \[ \]
  / image                                                      

  Configuration     `{{VERSION}}`            `{{URL}}`         \[ \]
  bundle                                                       

  Infrastructure    `{{COMMIT / PLAN ID}}`   `{{URL}}`         \[ \]
  plan                                                         

  Database          `{{VERSION}}`            `{{PATH}}`        \[ \]
  migration                                                    

  SBOM / provenance `{{REFERENCE}}`          `{{URL}}`         \[ \]
  / signature                                                  
  ------------------------------------------------------------------------------

**Artifact rule:** Record image digests or checksums, not only mutable
tags such as `latest`.

## 3. People, Roles and Communications

  -----------------------------------------------------------------------
  Role              Owner / contact   Responsibility    Decision
                                                        authority
  ----------------- ----------------- ----------------- -----------------
  Change / Release  `{{NAME}}`        Coordinates       Change window
  Manager                             change            

  Deployment        `{{NAME}}`        Executes approved Stop execution
  Operator                            steps             

  Technical Owner   `{{NAME}}`        Technical         Technical Go /
                                      validation        No-Go

  Incident          `{{NAME}}`        Coordinates       Rollback /
  Commander                           incident          escalation

  Security Approver `{{NAME}}`        Security          Security approval
                                      exceptions /      
                                      controls          

  Operations /      `{{NAME}}`        Monitoring and    Operational
  On-call                             handover          acceptance

  Business Owner    `{{NAME}}`        Business          Business
                                      validation        acceptance
  -----------------------------------------------------------------------

-   War-room / communication channel: `{{CHANNEL}}`
-   Status update cadence: `{{INTERVAL}}`
-   Customer / stakeholder notice owner: `{{OWNER}}`
-   Escalation contacts: `{{LINK}}`

## 4. Target Environment and Prerequisites

  ------------------------------------------------------------------------------------------------
  Area                    Target configuration                             Verified
  ----------------------- ------------------------------------------------ -----------------------
  Platform / hosting      `{{VM / CONTAINER / K8S / SERVERLESS / SAAS}}`   \[ \]

  Region / site / cluster `{{LOCATION}}`                                   \[ \]

  Runtime / OS /          `{{VERSIONS}}`                                   \[ \]
  framework                                                                

  CPU / memory / storage  `{{CAPACITY}}`                                   \[ \]

  Network / firewall /    `{{RULES}}`                                      \[ \]
  egress                                                                   

  DNS / endpoint          `{{HOSTNAME}}`                                   \[ \]

  TLS / certificates      `{{CERT / EXPIRY / OWNER}}`                      \[ \]

  Database / queue /      `{{SERVICE / VERSION}}`                          \[ \]
  cache                                                                    

  IAM / service identity  `{{IDENTITY}}`                                   \[ \]

  Scaling / availability  `{{POLICY}}`                                     \[ \]

  Monitoring / alerting   `{{DASHBOARD / ALERTS}}`                         \[ \]
  ------------------------------------------------------------------------------------------------

### 4.1 Environment matrix

  ------------------------------------------------------------------------------
  Environment    Purpose         Configuration   Data             Access
                                 source          classification   
  -------------- --------------- --------------- ---------------- --------------
  Development    `{{PURPOSE}}`   `{{SOURCE}}`    Synthetic        `{{ACCESS}}`

  QA / Test      `{{PURPOSE}}`   `{{SOURCE}}`    Test / masked    `{{ACCESS}}`

  Staging        `{{PURPOSE}}`   `{{SOURCE}}`    Controlled       `{{ACCESS}}`

  Production     `{{PURPOSE}}`   `{{SOURCE}}`    Live             Restricted
  ------------------------------------------------------------------------------

## 5. Pre-Deployment Quality Gates

### 5.1 Engineering gates

-   [ ] Pull request reviewed and approved.
-   [ ] Required unit, integration, contract, and end-to-end tests
    passed.
-   [ ] Static analysis, formatting, and type checks passed.
-   [ ] Dependency and vulnerability scans reviewed.
-   [ ] Secret scanning passed.
-   [ ] Build is reproducible and artifact provenance verified.
-   [ ] Performance / capacity acceptance criteria met.
-   [ ] Release notes and known limitations published.
-   [ ] No open release-blocking defects.

### 5.2 Security gates

-   [ ] Deployment identity uses least privilege.
-   [ ] Secrets are externalized and access is audited.
-   [ ] TLS and certificate chain / expiry validated.
-   [ ] Ingress and egress rules reviewed.
-   [ ] Required security approvals and exceptions recorded.
-   [ ] Container / package / host baseline reviewed.
-   [ ] Audit logging and incident alerting enabled.
-   [ ] Sensitive data is not exposed in logs or deployment output.

### 5.3 Operational gates

-   [ ] Staging validation completed.
-   [ ] Backup and restore / recovery path verified.
-   [ ] Monitoring, dashboards, and alert routes operational.
-   [ ] Runbook and rollback instructions reviewed.
-   [ ] On-call / escalation owner confirmed.
-   [ ] Change window and dependencies confirmed.
-   [ ] Capacity and quota checks completed.
-   [ ] Stakeholders informed.

## 6. Configuration and Secrets

  ----------------------------------------------------------------------------------------------------
  Setting / secret Purpose         Source                                Required       Validation
  key                                                                                   
  ---------------- --------------- ------------------------------------- -------------- --------------
  `{{KEY_NAME}}`   `{{PURPOSE}}`   `{{SECRET STORE / CONFIG SERVICE}}`   Yes / No       `{{RULE}}`

  ----------------------------------------------------------------------------------------------------

**Never store actual secret values in this document, tickets, source
control, screenshots, or logs.**

-   Configuration version: `{{VERSION}}`
-   Secret rotation / expiry owner: `{{OWNER}}`
-   Runtime config reload behavior: `{{BEHAVIOR}}`
-   Required restart: `{{YES / NO / DETAILS}}`

## 7. Data Migration and Backup Plan

-   Migration required: `{{YES / NO}}`
-   Migration owner: `{{OWNER}}`
-   Expected duration: `{{DURATION}}`
-   Backward compatibility: `{{DETAILS}}`
-   Lock / downtime risk: `{{DETAILS}}`
-   Backup ID and timestamp: `{{REFERENCE}}`
-   Restore test evidence: `{{REFERENCE}}`
-   RPO / RTO: `{{TARGETS}}`
-   Rollback feasibility: `{{YES / NO / LIMITATIONS}}`
-   Roll-forward / compensation plan: `{{DETAILS}}`

### 7.1 Migration steps

  ------------------------------------------------------------------------------------------
  Order          Action                    Owner          Verification /   Abort condition
                                                          evidence         
  -------------- ------------------------- -------------- ---------------- -----------------
  1              `{{BACKUP / SNAPSHOT}}`   `{{OWNER}}`    `{{EVIDENCE}}`   `{{CONDITION}}`

  2              `{{MIGRATION}}`           `{{OWNER}}`    `{{EVIDENCE}}`   `{{CONDITION}}`

  3              `{{RECONCILIATION}}`      `{{OWNER}}`    `{{EVIDENCE}}`   `{{CONDITION}}`
  ------------------------------------------------------------------------------------------

## 8. Deployment Strategy and Cutover

-   **Strategy:** `{{STRATEGY}}`
-   **Reason:** `{{RATIONALE / ADR}}`
-   **Traffic / workload shift:** `{{PERCENTAGE / METHOD}}`
-   **Canary evaluation period:** `{{DURATION}}`
-   **Feature flags:** `{{FLAGS / DEFAULTS}}`
-   **Parallel-run / shadow mode:** `{{DETAILS}}`
-   **Compatibility requirements:** `{{DETAILS}}`
-   **Cutover approver:** `{{NAME / ROLE}}`

### 8.1 Deployment flow

``` mermaid
flowchart TD
    A[Approved Change] --> B[Pre-flight Checks]
    B --> C{All Gates Pass?}
    C -- No --> X[No-Go / Stop]
    C -- Yes --> D[Deploy to Staging / Validate]
    D --> E{Staging Accepted?}
    E -- No --> X
    E -- Yes --> F[Production Backup / Snapshot]
    F --> G[Deploy Canary / Initial Scope]
    G --> H[Observe Metrics and Smoke Tests]
    H --> I{Healthy?}
    I -- No --> R[Rollback / Mitigate]
    I -- Yes --> J[Expand Rollout]
    J --> K[Full Production Validation]
    K --> L{Business and Ops Accepted?}
    L -- No --> R
    L -- Yes --> M[Handover and Close Change]
```

### 8.2 Execution steps

  -----------------------------------------------------------------------------------------
  Step           Action / command reference  Expected result  Owner          Evidence
  -------------- --------------------------- ---------------- -------------- --------------
  1              `{{PREFLIGHT}}`             `{{EXPECTED}}`   `{{OWNER}}`    `{{LINK}}`

  2              `{{BACKUP}}`                `{{EXPECTED}}`   `{{OWNER}}`    `{{LINK}}`

  3              `{{DEPLOY}}`                `{{EXPECTED}}`   `{{OWNER}}`    `{{LINK}}`

  4              `{{MIGRATE / CONFIGURE}}`   `{{EXPECTED}}`   `{{OWNER}}`    `{{LINK}}`

  5              `{{SMOKE TEST}}`            `{{EXPECTED}}`   `{{OWNER}}`    `{{LINK}}`

  6              `{{TRAFFIC / ENABLE}}`      `{{EXPECTED}}`   `{{OWNER}}`    `{{LINK}}`
  -----------------------------------------------------------------------------------------

Commands MUST be verified for the actual OS, shell, runtime,
permissions, and target. Do not paste unreviewed destructive commands.

## 9. CI/CD and Release Controls

  -------------------------------------------------------------------------
  Stage             Required control  Evidence          Result
  ----------------- ----------------- ----------------- -------------------
  Source            Protected branch  `{{LINK}}`        `{{PASS / FAIL}}`
                    / approved tag                      

  Build             Reproducible      `{{LINK}}`        `{{PASS / FAIL}}`
                    build                               

  Tests             Required test     `{{LINK}}`        `{{PASS / FAIL}}`
                    suites / coverage                   
                    policy                              

  Security          SAST / SCA /      `{{LINK}}`        `{{PASS / FAIL}}`
                    secret scan /                       
                    image scan                          

  Artifact          Immutable         `{{LINK}}`        `{{PASS / FAIL}}`
                    artifact /                          
                    signature / SBOM                    

  Approval          Authorized        `{{LINK}}`        `{{PASS / FAIL}}`
                    release approval                    

  Deployment        Controlled        `{{LINK}}`        `{{PASS / FAIL}}`
                    promotion                           

  Verification      Smoke / SLO /     `{{LINK}}`        `{{PASS / FAIL}}`
                    business                            
                    validation                          
  -------------------------------------------------------------------------

## 10. Post-Deployment Verification

### 10.1 Platform / technical checks

-   [ ] Expected version, commit, package, or image digest is active.
-   [ ] Service / process / pods / workers are healthy.
-   [ ] Readiness and liveness checks pass.
-   [ ] CPU, memory, disk, network, and queue depth are within limits.
-   [ ] Database and external dependencies are reachable.
-   [ ] TLS, DNS, routing, and authentication work.
-   [ ] No new critical error patterns in logs.
-   [ ] Scheduled jobs and background workers are operating.

### 10.2 Functional smoke tests

  ----------------------------------------------------------------------------------------------------
  Test ID     Scenario              Expected         Actual           Result              Evidence
  ----------- --------------------- ---------------- ---------------- ------------------- ------------
  SM-001      `{{CRITICAL FLOW}}`   `{{EXPECTED}}`   `{{OBSERVED}}`   `{{PASS / FAIL}}`   `{{LINK}}`

  ----------------------------------------------------------------------------------------------------

### 10.3 Business / data validation

-   [ ] Critical business transaction / workflow completed.
-   [ ] Data counts, checksums, totals, or reconciliation validated.
-   [ ] No duplicate, missing, or unexpected records.
-   [ ] Business owner accepted output.
-   [ ] User / customer impact assessed.

## 11. SLO, Monitoring and Observation Window

  -----------------------------------------------------------------------------
  Signal                Baseline Threshold / SLO        Observed Decision
  -------------- --------------- --------------- --------------- --------------
  Availability       `{{VALUE}}`    `{{TARGET}}`     `{{VALUE}}` `{{ACTION}}`

  Error rate         `{{VALUE}}`    `{{TARGET}}`     `{{VALUE}}` `{{ACTION}}`

  Latency            `{{VALUE}}`    `{{TARGET}}`     `{{VALUE}}` `{{ACTION}}`

  Resource usage     `{{VALUE}}`    `{{TARGET}}`     `{{VALUE}}` `{{ACTION}}`

  Queue / job        `{{VALUE}}`    `{{TARGET}}`     `{{VALUE}}` `{{ACTION}}`
  backlog                                                        
  -----------------------------------------------------------------------------

-   Observation duration: `{{DURATION}}`
-   Dashboard: `{{LINK}}`
-   Alert channel: `{{CHANNEL}}`
-   On-call owner: `{{OWNER}}`

## 12. Rollback and Recovery

### 12.1 Predefined rollback triggers

  ------------------------------------------------------------------------------------
  Trigger             Threshold / condition        Detection source  Decision owner
  ------------------- ---------------------------- ----------------- -----------------
  Critical health     `{{CONDITION}}`              `{{SOURCE}}`      `{{OWNER}}`
  check failure                                                      

  Error rate /        `{{THRESHOLD + DURATION}}`   `{{SOURCE}}`      `{{OWNER}}`
  latency breach                                                     

  Data integrity      `{{CONDITION}}`              `{{SOURCE}}`      `{{OWNER}}`
  failure                                                            

  Security incident   `{{CONDITION}}`              `{{SOURCE}}`      `{{OWNER}}`

  Business-critical   `{{CONDITION}}`              `{{SOURCE}}`      `{{OWNER}}`
  workflow failure                                                   
  ------------------------------------------------------------------------------------

### 12.2 Rollback prerequisites

-   Previous known-good artifact: `{{VERSION / DIGEST}}`
-   Previous configuration: `{{VERSION}}`
-   Database recovery method: `{{METHOD}}`
-   Traffic restoration method: `{{METHOD}}`
-   Required approver / incident commander: `{{ROLE}}`
-   Estimated rollback duration: `{{DURATION}}`
-   Known irreversible actions: `{{DETAILS}}`

### 12.3 Rollback procedure

  --------------------------------------------------------------------------
  Order          Action         Owner          Expected       Verification
                                               result         
  -------------- -------------- -------------- -------------- --------------
  1              Stop / pause   `{{OWNER}}`    No new changes `{{CHECK}}`
                 rollout and                                  
                 triggers                                     

  2              Restore        `{{OWNER}}`    Known-good     `{{CHECK}}`
                 previous                      version active 
                 artifact /                                   
                 route                                        

  3              Restore        `{{OWNER}}`    Config valid   `{{CHECK}}`
                 compatible                                   
                 config                                       

  4              Recover /      `{{OWNER}}`    Data integrity `{{CHECK}}`
                 reconcile data                restored       
                 if needed                                    

  5              Run smoke      `{{OWNER}}`    Service stable `{{CHECK}}`
                 tests and                                    
                 notify                                       
  --------------------------------------------------------------------------

**Database warning:** A code rollback does not necessarily reverse a
schema migration or external side effect. Prefer backward-compatible
expand/contract migrations and document roll-forward or compensating
actions.

Full rollback runbook: `{{ROLLBACK_DOC_LINK}}`

## 13. Incident Response and Escalation

  Severity   Definition              Response target   Owner / channel
  ---------- ----------------------- ----------------- -----------------
  SEV-1      `{{CRITICAL IMPACT}}`   `{{TARGET}}`      `{{OWNER}}`
  SEV-2      `{{MAJOR IMPACT}}`      `{{TARGET}}`      `{{OWNER}}`
  SEV-3      `{{LIMITED IMPACT}}`    `{{TARGET}}`      `{{OWNER}}`

Incident commander: `{{NAME}}`\
Status update cadence: `{{INTERVAL}}`\
Customer / stakeholder communication owner: `{{NAME}}`

## 14. Specialized Deployment Controls

### 14.1 Python automation

-   [ ] Runtime and dependency lockfile verified.
-   [ ] Virtual environment / container / executable build verified.
-   [ ] Service account and SSH / API / database credentials scoped.
-   [ ] Scheduler timezone, overlap policy, working directory, and
    environment verified.
-   [ ] Dry-run / safe-mode tested.
-   [ ] Target allowlist, batch size, concurrency, and rate limits
    configured.
-   [ ] Run ID, checkpoint, retry, and partial-failure behavior tested.
-   [ ] Post-change state validation and evidence capture enabled.
-   [ ] Stop / resume / recovery instructions available.

### 14.2 MCP server

-   [ ] MCP SDK and protocol compatibility verified against supported
    clients.
-   [ ] Transport, endpoint, TLS, and authentication configured.
-   [ ] Tool schemas and server-side argument validation tested.
-   [ ] Authorization enforced for every protected tool call.
-   [ ] Read-only and mutating tools clearly separated.
-   [ ] Tool timeouts, quotas, concurrency, and payload limits
    configured.
-   [ ] Health / readiness checks and structured logs verified.
-   [ ] Destructive tools require explicit approval.
-   [ ] Tool output is redacted and safe for model context.
-   [ ] Client interoperability smoke tests passed.

### 14.3 AI agent / LLM application

-   [ ] Model provider, model identifier, prompt, and policy versions
    recorded.
-   [ ] Provider credentials stored securely.
-   [ ] Token, cost, latency, and iteration budgets configured.
-   [ ] Tool allowlist and permission scopes verified.
-   [ ] Human approval gates tested for consequential actions.
-   [ ] Prompt injection and untrusted retrieval tests passed.
-   [ ] PII / sensitive data handling and retention reviewed.
-   [ ] Model fallback / provider outage behavior tested.
-   [ ] Evaluation suite and quality thresholds passed.
-   [ ] Agent traceability and audit events enabled.

## 15. Operational Handover

  Handover item                       Location / owner   Accepted
  ----------------------------------- ------------------ ----------
  Architecture and diagrams           `{{LINK}}`         \[ \]
  Deployment and rollback runbook     `{{LINK}}`         \[ \]
  Monitoring dashboard / alerts       `{{LINK}}`         \[ \]
  Backup / restore instructions       `{{LINK}}`         \[ \]
  Configuration / secrets ownership   `{{OWNER}}`        \[ \]
  Known issues / workarounds          `{{LINK}}`         \[ \]
  Support / escalation contacts       `{{LINK}}`         \[ \]
  Access / break-glass procedure      `{{LINK}}`         \[ \]

## 16. Go / No-Go Decision

  Gate                 Owner         Status                   Evidence
  -------------------- ------------- ------------------------ ------------
  Quality / test       `{{OWNER}}`   `{{GO / NO-GO}}`         `{{LINK}}`
  Security             `{{OWNER}}`   `{{GO / NO-GO / N/A}}`   `{{LINK}}`
  Data / backup        `{{OWNER}}`   `{{GO / NO-GO / N/A}}`   `{{LINK}}`
  Operations           `{{OWNER}}`   `{{GO / NO-GO}}`         `{{LINK}}`
  Business             `{{OWNER}}`   `{{GO / NO-GO}}`         `{{LINK}}`
  Rollback readiness   `{{OWNER}}`   `{{GO / NO-GO}}`         `{{LINK}}`

**Final decision:** `{{GO / NO-GO}}`\
**Decision maker:** `{{NAME / ROLE}}`\
**Timestamp and timezone:** `{{TIMESTAMP}}`\
**Conditions / rationale:** `{{DETAILS}}`

## 17. Deployment Execution Log

  --------------------------------------------------------------------------
  Timestamp +    Step / action  Operator       Outcome        Evidence /
  timezone                                                    ticket
  -------------- -------------- -------------- -------------- --------------
  `{{TIME}}`     `{{ACTION}}`   `{{NAME}}`     `{{RESULT}}`   `{{LINK}}`

  --------------------------------------------------------------------------

## 18. Final Outcome and Sign-off

-   **Final status:**
    `{{SUCCESS / SUCCESS WITH ISSUES / ROLLED BACK / FAILED}}`
-   **Actual start / finish:** `{{TIMESTAMPS}}`
-   **Downtime / impact:** `{{DETAILS}}`
-   **Issues / deviations:** `{{DETAILS}}`
-   **Follow-up actions:** `{{ACTIONS + OWNERS + DATES}}`
-   **Change record:** `{{LINK}}`

  Approver          Name         Decision               Date
  ----------------- ------------ ---------------------- ------------
  Technical Owner   `{{NAME}}`   `{{ACCEPTED}}`         `{{DATE}}`
  Operations        `{{NAME}}`   `{{ACCEPTED}}`         `{{DATE}}`
  Security          `{{NAME}}`   `{{ACCEPTED / N/A}}`   `{{DATE}}`
  Business Owner    `{{NAME}}`   `{{ACCEPTED}}`         `{{DATE}}`

------------------------------------------------------------------------

## Appendix A --- Production Go-Live Checklist

-   [ ] Change approved and deployment window confirmed.
-   [ ] Artifact identity, integrity, and provenance verified.
-   [ ] Quality and security gates passed.
-   [ ] Production configuration and secrets verified securely.
-   [ ] Backup / restore and migration strategy confirmed.
-   [ ] Deployment plan and stop conditions reviewed.
-   [ ] Smoke tests and business validation passed.
-   [ ] Monitoring, alerting, and on-call coverage confirmed.
-   [ ] Rollback / recovery path is actionable.
-   [ ] Operations handover accepted.
-   [ ] Execution evidence and final sign-off recorded.

**End of template.** A successful deployment requires verified outcomes,
not merely a successful deployment command.