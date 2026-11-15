# Enterprise Design & Architecture Standard --- V2.0

> **Document type:** Reusable engineering template\
> **Scope:** Technology-agnostic; with optional deep-dive guidance for
> Python automation, MCP servers, AI agents, APIs, data pipelines, and
> infrastructure systems.\
> **Status:** Template --- complete, tailor, review, and approve before
> implementation.

------------------------------------------------------------------------

## Document Control

  Field                      Value
  -------------------------- ---------------------------------------------
  Project / Product          `{{PROJECT_NAME}}`
  Document ID                `{{DOC_ID}}`
  Version                    `2.0`
  Status                     `Draft / In Review / Approved / Superseded`
  Author / Owner             `{{OWNER}}`
  Reviewers                  `{{REVIEWERS}}`
  Created / Updated          `{{YYYY-MM-DD}}`
  Target release             `{{RELEASE}}`
  Repository / Project URL   `{{URL}}`
  Related documents          `{{LINKS}}`

### Change history

  Version   Date         Author         Summary
  --------- ------------ -------------- -------------------------------
  2.0       `{{DATE}}`   `{{AUTHOR}}`   Advanced engineering standard

## 0. Instructions for Humans and AI Coding Agents

### 0.1 Normative language

The words **MUST**, **MUST NOT**, **REQUIRED**, **SHOULD**, **SHOULD
NOT**, and **MAY** express requirement strength:

-   MUST / MUST NOT: mandatory engineering or safety requirement.
-   SHOULD / SHOULD NOT: recommended unless a documented exception
    exists.
-   MAY: optional.

### 0.2 Documentation rules

1.  Discover the actual repository, code, manifests, tests, workflows,
    and infrastructure before describing the current system.
2.  Do not invent technologies, endpoints, environment variables,
    commands, service names, performance numbers, owners, or security
    controls.
3.  Mark unknown facts as `TBD — owner: {{OWNER}} — due: {{DATE}}`.
4.  Distinguish **current state**, **proposed target state**, and
    **future options**.
5.  Link significant decisions to ADRs; do not bury decision rationale
    in architecture diagrams.
6.  Prefer diagrams, tables, and concrete examples over long generic
    prose.
7.  Keep architecture documentation synchronized with code and
    configuration changes.
8.  Remove unused sections or mark them `N/A — reason: ...`; do not
    leave misleading boilerplate.
9.  Every diagram, schema, and referenced artifact MUST have a path or
    stable link.
10. AI-generated documentation MUST be reviewed by a responsible
    engineer before approval.

### 0.3 Required discovery inputs

  Input                                     Location / Evidence   Status
  ----------------------------------------- --------------------- --------------
  Existing README and requirements          `{{PATH}}`            `{{STATUS}}`
  Source tree and entry points              `{{PATH}}`            `{{STATUS}}`
  Dependency / build manifests              `{{PATH}}`            `{{STATUS}}`
  Tests and fixtures                        `{{PATH}}`            `{{STATUS}}`
  CI/CD workflows                           `{{PATH}}`            `{{STATUS}}`
  Infrastructure / deployment definitions   `{{PATH}}`            `{{STATUS}}`
  Existing ADRs / runbooks                  `{{PATH}}`            `{{STATUS}}`
  Runtime configuration examples            `{{PATH}}`            `{{STATUS}}`

**Discovery limitation:** `{{NONE / DETAILS}}`

## 1. Executive Summary

-   **Problem statement:** `{{PROBLEM}}`
-   **Proposed solution:** `{{SOLUTION}}`
-   **Primary users / consumers:** `{{USERS}}`
-   **Business / operational value:** `{{VALUE}}`
-   **System boundary:** `{{BOUNDARY}}`
-   **Delivery approach:** `{{APPROACH}}`
-   **Top risks:** `{{RISKS}}`

## 2. Goals, Non-Goals and Success Criteria

### 2.1 Goals

  ID      Goal         Priority                  Success measure
  ------- ------------ ------------------------- -----------------
  G-001   `{{GOAL}}`   `Must / Should / Could`   `{{MEASURE}}`

### 2.2 Non-goals

-   `{{OUT_OF_SCOPE}}`

### 2.3 Measurable outcomes

  -----------------------------------------------------------------------------
  KPI / SLI              Baseline           Target Measurement    Owner
                                                   source         
  -------------- ---------------- ---------------- -------------- -------------
  `{{METRIC}}`        `{{VALUE}}`     `{{TARGET}}` `{{SOURCE}}`   `{{OWNER}}`

  -----------------------------------------------------------------------------

## 3. Stakeholders and Ownership

  -----------------------------------------------------------------------
  Role              Team / Person     Accountability    Approval
                                                        required?
  ----------------- ----------------- ----------------- -----------------
  Product /         `{{NAME}}`        Scope and         Yes
  Business Owner                      business          
                                      acceptance        

  Technical Owner / `{{NAME}}`        Architecture and  Yes
  Architect                           technical quality 

  Security Owner    `{{NAME}}`        Threats and       As applicable
                                      security controls 

  Platform /        `{{NAME}}`        Runtime and       As applicable
  Operations                          operational       
                                      readiness         

  Data Owner        `{{NAME}}`        Data quality,     As applicable
                                      access, retention 

  Developer /       `{{NAME}}`        Implementation    Yes
  Maintainer                          and support       
  -----------------------------------------------------------------------

## 4. Requirements Specification

### 4.1 Functional requirements

  ---------------------------------------------------------------------------------------
  ID             Requirement      Priority       Source         Acceptance criteria
  -------------- ---------------- -------------- -------------- -------------------------
  FR-001         The system MUST  Must           `{{SOURCE}}`   `{{TESTABLE_CRITERIA}}`
                 `{{BEHAVIOR}}`                                 

  ---------------------------------------------------------------------------------------

### 4.2 Non-functional requirements

  -------------------------------------------------------------------------------------
  Attribute               Requirement / target                  Verification method
  ----------------------- ------------------------------------- -----------------------
  Performance             `{{LATENCY / THROUGHPUT}}`            Load / benchmark test

  Availability            `{{SLO}}`                             Monitoring /
                                                                availability test

  Reliability             `{{RECOVERY / FAILURE TARGET}}`       Fault-injection /
                                                                recovery test

  Scalability             `{{EXPECTED GROWTH}}`                 Capacity test

  Security                `{{CONTROL REQUIREMENTS}}`            Threat review /
                                                                security test

  Privacy                 `{{DATA MINIMIZATION / RETENTION}}`   Privacy review

  Maintainability         `{{CODE / MODULE STANDARDS}}`         Review / static
                                                                analysis

  Portability             `{{SUPPORTED PLATFORMS}}`             Compatibility test

  Observability           `{{LOGS / METRICS / TRACES}}`         Operational validation

  Accessibility /         `{{STANDARD / EXPECTATION}}`          Usability test
  usability                                                     

  Cost                    `{{BUDGET / UNIT COST}}`              Cost monitoring
  -------------------------------------------------------------------------------------

### 4.3 Requirement traceability

  --------------------------------------------------------------------------------
  Requirement ID Design component  Implementation   Test ID         Status
                                   location                         
  -------------- ----------------- ---------------- --------------- --------------
  FR-001         `{{COMPONENT}}`   `{{PATH}}`       `{{TEST_ID}}`   `{{STATUS}}`

  --------------------------------------------------------------------------------

## 5. Constraints, Assumptions and Dependencies

### 5.1 Constraints

  -----------------------------------------------------------------------------------------------------
  Constraint         Type                                           Impact            Mitigation /
                                                                                      workaround
  ------------------ ---------------------------------------------- ----------------- -----------------
  `{{CONSTRAINT}}`   `Technical / Business / Legal / Operational`   `{{IMPACT}}`      `{{PLAN}}`

  -----------------------------------------------------------------------------------------------------

### 5.2 Assumptions

  Assumption         Validation method   Owner         Due date
  ------------------ ------------------- ------------- ------------
  `{{ASSUMPTION}}`   `{{METHOD}}`        `{{OWNER}}`   `{{DATE}}`

### 5.3 External dependencies

  ----------------------------------------------------------------------------------------------
  Dependency                      Provider /     Contract /      Failure impact Fallback
                                  owner          version                        
  ------------------------------- -------------- --------------- -------------- ----------------
  `{{API / SERVICE / DATASET}}`   `{{OWNER}}`    `{{VERSION}}`   `{{IMPACT}}`   `{{FALLBACK}}`

  ----------------------------------------------------------------------------------------------

## 6. Architecture Principles and Quality Attributes

Record project-specific principles. Typical defaults:

1.  **Separation of concerns:** domain logic MUST be separated from
    transport, persistence, and vendor-specific adapters.
2.  **Least privilege:** each identity, service, agent, and tool MUST
    have only the permissions it needs.
3.  **Secure by default:** insecure modes MUST NOT be enabled implicitly
    in production.
4.  **Configuration outside code:** environment-specific settings and
    secrets MUST be externalized.
5.  **Observable execution:** critical operations MUST emit actionable
    logs and measurable outcomes.
6.  **Recoverability:** state-changing workflows SHOULD support
    checkpoints, idempotency, compensation, or a documented recovery
    path.
7.  **Explicit contracts:** API, event, tool, and data schemas SHOULD be
    versioned and validated.
8.  **Simplicity:** prefer the least complex design that satisfies
    requirements.

### 6.1 Quality attribute scenarios

  -----------------------------------------------------------------------------
  Attribute         Stimulus          Expected response       Measure /
                                                              threshold
  ----------------- ----------------- ----------------------- -----------------
  `{{ATTRIBUTE}}`   `{{EVENT}}`       `{{SYSTEM_RESPONSE}}`   `{{MEASURE}}`

  -----------------------------------------------------------------------------

## 7. System Context and Boundaries

### 7.1 Context diagram

``` mermaid
flowchart LR
    USER[Users / Triggering Systems] --> SYS[System Under Design]
    SYS --> DATA[(Owned Data Stores)]
    SYS --> EXT[External APIs / Services]
    OPS[Operations / Monitoring] -.-> SYS
    IDP[Identity Provider] --> SYS
```

Replace every illustrative component with verified system elements.

### 7.2 System boundary

-   **Owned by this system:** `{{RESPONSIBILITIES}}`
-   **Outside the boundary:** `{{EXTERNAL_RESPONSIBILITIES}}`
-   **Trust boundaries:** `{{BOUNDARIES}}`
-   **Sensitive data crossing boundaries:** `{{DATA}}`

## 8. Architecture Style and Views

-   **Selected style:**
    `{{Layered / Modular monolith / Microservices / Event-driven / Serverless / Hybrid}}`
-   **Rationale / ADR:** `{{ADR_LINK}}`
-   **Alternatives considered:** `{{ALTERNATIVES}}`
-   **Known trade-offs:** `{{TRADE_OFFS}}`

### 8.1 Logical / component view

  ------------------------------------------------------------------------------------
  Component         Responsibility   Interface         Data owned     Failure behavior
  ----------------- ---------------- ----------------- -------------- ----------------
  `{{COMPONENT}}`   `{{PURPOSE}}`    `{{INTERFACE}}`   `{{DATA}}`     `{{BEHAVIOR}}`

  ------------------------------------------------------------------------------------

``` mermaid
flowchart TB
    ENTRY[Entry Point / API] --> APP[Application / Use Cases]
    APP --> DOMAIN[Domain / Business Rules]
    APP --> PORTS[Ports / Interfaces]
    PORTS --> ADAPTERS[External Adapters]
    APP --> REPO[Repository / Persistence]
    APP --> OBS[Observability]
```

### 8.2 Runtime / sequence view

``` mermaid
sequenceDiagram
    participant C as Client / Trigger
    participant A as Application
    participant D as Domain Logic
    participant X as External Dependency
    C->>A: Request / event
    A->>A: Validate identity and input
    A->>D: Execute use case
    D->>X: Call dependency through adapter
    X-->>D: Result / error
    D-->>A: Domain outcome
    A-->>C: Response / acknowledgement
```

### 8.3 Deployment / physical view

``` mermaid
flowchart TB
    CLIENT[Client / Scheduler] --> EDGE[Ingress / Gateway]
    EDGE --> APP[Application Runtime]
    APP --> STORE[(Database / Object Store)]
    APP --> QUEUE[Queue / Event Bus]
    APP --> OBS[Logs / Metrics / Traces]
    SECRETS[Secret Manager] --> APP
```

### 8.4 Data-flow inventory

  ------------------------------------------------------------------------------------------------
  Flow ID     Source         Destination         Data             Protocol         Protection
                                                 classification                    
  ----------- -------------- ------------------- ---------------- ---------------- ---------------
  DF-001      `{{SOURCE}}`   `{{DESTINATION}}`   `{{CLASS}}`      `{{PROTOCOL}}`   `{{CONTROL}}`

  ------------------------------------------------------------------------------------------------

## 9. Component and Interface Contracts

For each component:

-   Name / identifier: `{{NAME}}`
-   Responsibility and explicit non-responsibilities: `{{DETAILS}}`
-   Input schema and validation: `{{SCHEMA}}`
-   Output schema and invariants: `{{SCHEMA}}`
-   Dependencies and timeouts: `{{DEPENDENCIES}}`
-   Error contract: `{{ERRORS}}`
-   Authorization boundary: `{{PERMISSIONS}}`
-   Observability requirements: `{{LOGS / METRICS}}`
-   Versioning / compatibility: `{{POLICY}}`

## 10. API, Events and Integration Design

  Contract                      Details
  ----------------------------- ---------------------------------------
  Interface name / version      `{{NAME}}`
  Producer / consumer           `{{SYSTEMS}}`
  Protocol / transport          `{{REST / RPC / EVENT / FILE / MCP}}`
  Schema / contract location    `{{PATH / URL}}`
  Authentication                `{{METHOD}}`
  Authorization                 `{{SCOPE / ROLE}}`
  Timeout / deadline            `{{DURATION}}`
  Retry / backoff               `{{POLICY}}`
  Rate limit / quota            `{{LIMIT}}`
  Idempotency / deduplication   `{{METHOD}}`
  Pagination / batching         `{{METHOD}}`
  Error mapping                 `{{CONTRACT}}`
  Compatibility policy          `{{POLICY}}`

Breaking changes MUST have a migration and compatibility plan.

## 11. Data Architecture and Governance

### 11.1 Data inventory

  -----------------------------------------------------------------------------
  Dataset /       Source of      Owner          Classification   Retention
  entity          truth                                          
  --------------- -------------- -------------- ---------------- --------------
  `{{DATASET}}`   `{{SOURCE}}`   `{{OWNER}}`    `{{CLASS}}`      `{{PERIOD}}`

  -----------------------------------------------------------------------------

### 11.2 Data model / dictionary

  ---------------------------------------------------------------------------------------
  Entity /      Type         Nullable       Constraint   Description     Classification
  field                                                                  
  ------------- ------------ -------------- ------------ --------------- ----------------
  `{{FIELD}}`   `{{TYPE}}`   `{{YES/NO}}`   `{{RULE}}`   `{{MEANING}}`   `{{CLASS}}`

  ---------------------------------------------------------------------------------------

### 11.3 Data lifecycle

-   Ingestion: `{{PROCESS}}`
-   Validation / quality checks: `{{PROCESS}}`
-   Storage / encryption: `{{PROCESS}}`
-   Access / audit: `{{PROCESS}}`
-   Retention / archival: `{{POLICY}}`
-   Deletion / right-to-erasure where applicable: `{{PROCESS}}`
-   Backup / restore / RPO / RTO: `{{DETAILS}}`

## 12. Security Architecture and Threat Model

### 12.1 Security controls

  Control area                      Design / implementation   Evidence / verification
  --------------------------------- ------------------------- -------------------------
  Authentication                    `{{DESIGN}}`              `{{TEST / CONFIG}}`
  Authorization / RBAC / ABAC       `{{DESIGN}}`              `{{TEST}}`
  Secrets / key management          `{{DESIGN}}`              `{{SCAN / REVIEW}}`
  Encryption in transit / at rest   `{{DESIGN}}`              `{{CONFIG}}`
  Network segmentation / egress     `{{DESIGN}}`              `{{RULES}}`
  Input validation                  `{{DESIGN}}`              `{{TEST}}`
  Audit trail                       `{{DESIGN}}`              `{{LOG EVIDENCE}}`
  Dependency / supply chain         `{{DESIGN}}`              `{{SBOM / SCAN}}`
  Privacy / data minimization       `{{DESIGN}}`              `{{REVIEW}}`

### 12.2 Threat register

  ------------------------------------------------------------------------------------------------------------
  ID       Asset         Threat /       Likelihood    Impact        Mitigation      Residual     Owner
                         attack path                                                risk         
  -------- ------------- -------------- ------------- ------------- --------------- ------------ -------------
  T-001    `{{ASSET}}`   `{{THREAT}}`   `{{L/M/H}}`   `{{L/M/H}}`   `{{CONTROL}}`   `{{RISK}}`   `{{OWNER}}`

  ------------------------------------------------------------------------------------------------------------

Threat modelling SHOULD cover trust boundaries, spoofing, tampering,
repudiation, information disclosure, denial of service, and privilege
escalation.

## 13. Optional Specialization: Python Automation

Complete when Python is used:

-   Supported Python version(s): `{{VERSIONS}}`
-   Package / dependency manager and lockfile: `{{TOOL}}`
-   Runtime / OS support: `{{PLATFORMS}}`
-   Entry point and execution mode: `{{CLI / API / CRON / WORKER}}`
-   Module boundaries: `{{MODULES}}`
-   Configuration validation: `{{METHOD}}`
-   Structured logging / correlation ID: `{{METHOD}}`
-   Resource lifecycle (SSH, HTTP, DB, files): `{{METHOD}}`
-   Concurrency / worker limits: `{{LIMITS}}`
-   Packaging / distribution: `{{WHEEL / CONTAINER / EXE}}`
-   Test and quality tooling: `{{TOOLS}}`

### 13.1 Automation safety design

-   Target inventory and allowlist: `{{SOURCE}}`
-   Pre-checks: `{{CONNECTIVITY / VERSION / STATE}}`
-   Dry-run / preview: `{{BEHAVIOR}}`
-   Change approval: `{{APPROVAL}}`
-   Rate / concurrency limits: `{{LIMITS}}`
-   Checkpoint / resume: `{{METHOD}}`
-   Post-checks: `{{VALIDATION}}`
-   Rollback / compensation: `{{METHOD}}`

## 14. Optional Specialization: MCP Server

### 14.1 Server definition

  Item                          Design
  ----------------------------- -------------------------------------------------
  Server name / purpose         `{{NAME}}`
  MCP SDK / framework version   `{{VERSION}}`
  Transport                     `{{STDIO / STREAMABLE HTTP / OTHER SUPPORTED}}`
  Hosting / runtime             `{{RUNTIME}}`
  Client compatibility tested   `{{CLIENTS / VERSIONS}}`
  Authentication                `{{METHOD}}`
  Authorization model           `{{MODEL}}`
  Health / readiness            `{{ENDPOINT / METHOD}}`
  Session / state model         `{{STATE}}`

### 14.2 MCP primitive inventory

  -------------------------------------------------------------------------------------------------------------
  Name         Primitive                    Purpose         Input / output Permission    Side effects
                                                            schema                       
  ------------ ---------------------------- --------------- -------------- ------------- ----------------------
  `{{NAME}}`   `Tool / Resource / Prompt`   `{{PURPOSE}}`   `{{SCHEMA}}`   `{{SCOPE}}`   `{{NONE / DETAILS}}`

  -------------------------------------------------------------------------------------------------------------

MCP tools MUST validate arguments server-side. Tool descriptions and
schemas are not security controls.

### 14.3 MCP trust and safety

-   Treat tool arguments, resource contents, retrieved documents, and
    remote tool results as untrusted.
-   Enforce identity and authorization on every protected operation.
-   Use explicit allowlists for tools and target systems.
-   Apply deadlines, payload limits, concurrency caps, and rate limits.
-   Require confirmation for destructive, financial, privileged, or
    externally visible actions.
-   Prevent secrets from appearing in tool output, traces, or model
    context.
-   Separate read-only tools from state-changing tools.
-   Audit actor, tool, target, decision, and outcome without recording
    secret payloads.

## 15. Optional Specialization: AI Agent / LLM System

### 15.1 Agent contract

  Field                             Design
  --------------------------------- ------------------
  Agent name / role                 `{{NAME}}`
  Mission                           `{{PURPOSE}}`
  Explicitly permitted actions      `{{ALLOWLIST}}`
  Prohibited actions                `{{DENYLIST}}`
  Model provider / model ID         `{{MODEL}}`
  Prompt / policy version           `{{VERSION}}`
  Tools / MCP servers               `{{TOOLS}}`
  Context sources                   `{{SOURCES}}`
  Memory / state retention          `{{POLICY}}`
  Human approval gates              `{{CONDITIONS}}`
  Max steps / time / token / cost   `{{BUDGETS}}`
  Stop / escalation conditions      `{{RULES}}`

### 15.2 Agent execution flow

``` mermaid
flowchart TD
    U[User Request] --> P[Policy and Input Validation]
    P --> C[Build Context]
    C --> M[Model / Planner]
    M --> D{Needs Tool?}
    D -- No --> V[Validate Final Answer]
    D -- Yes --> A[Authorize Tool and Arguments]
    A --> H{Human Approval Required?}
    H -- Yes --> AP[Request Approval]
    H -- No --> X[Execute Tool]
    AP -->|Approved| X
    AP -->|Rejected| S[Stop Safely]
    X --> R[Validate Tool Result]
    R --> L{Budget / Stop Condition Met?}
    L -- No --> M
    L -- Yes --> V
    V --> O[Return Answer and Audit Record]
```

### 15.3 AI evaluation plan

  --------------------------------------------------------------------------------
  Evaluation     Dataset /        Metric             Threshold      Owner
  area           scenario                                           
  -------------- ---------------- ------------------ -------------- --------------
  Task success   `{{DATASET}}`    `{{METRIC}}`       `{{TARGET}}`   `{{OWNER}}`

  Tool selection `{{DATASET}}`    `{{METRIC}}`       `{{TARGET}}`   `{{OWNER}}`
  / argument                                                        
  correctness                                                       

  Groundedness / `{{DATASET}}`    `{{METRIC}}`       `{{TARGET}}`   `{{OWNER}}`
  factuality                                                        

  Prompt         `{{CASES}}`      `{{PASS RATE}}`    `{{TARGET}}`   `{{OWNER}}`
  injection                                                         
  resistance                                                        

  Unauthorized   `{{CASES}}`      `{{VIOLATIONS}}`   `0`            `{{OWNER}}`
  action                                                            
  prevention                                                        

  Cost / latency `{{WORKLOAD}}`   `{{METRIC}}`       `{{TARGET}}`   `{{OWNER}}`
  --------------------------------------------------------------------------------

Do not treat an LLM judge as the sole quality or safety control. Use
deterministic assertions for critical business rules.

## 16. Reliability, Resilience and Failure Analysis

  ---------------------------------------------------------------------------
  Failure mode    Detection      User /         Recovery       Data-loss risk
                                 business                      
                                 impact                        
  --------------- -------------- -------------- -------------- --------------
  `{{FAILURE}}`   `{{SIGNAL}}`   `{{IMPACT}}`   `{{ACTION}}`   `{{RISK}}`

  ---------------------------------------------------------------------------

Define: - Timeouts and end-to-end deadlines. - Retryable versus
permanent errors. - Exponential backoff and jitter where appropriate. -
Circuit breakers / bulkheads where appropriate. - Idempotency and
duplicate suppression. - Graceful degradation and fallback behavior. -
RPO, RTO, backup, restore, and disaster recovery. - Manual recovery and
escalation.

## 17. Deployment and Environment Design

  ---------------------------------------------------------------------------------------
  Environment   Purpose         Infrastructure   Data type    Access policy  Promotion
                                                                             gate
  ------------- --------------- ---------------- ------------ -------------- ------------
  Development   `{{PURPOSE}}`   `{{DETAILS}}`    Synthetic    `{{ACCESS}}`   `{{GATE}}`

  Test / QA     `{{PURPOSE}}`   `{{DETAILS}}`    Test /       `{{ACCESS}}`   `{{GATE}}`
                                                 masked                      

  Staging       `{{PURPOSE}}`   `{{DETAILS}}`    Controlled   `{{ACCESS}}`   `{{GATE}}`

  Production    `{{PURPOSE}}`   `{{DETAILS}}`    Live         Restricted     Approved
                                                                             release
  ---------------------------------------------------------------------------------------

Document network zones, DNS, TLS, compute, storage, scaling, secrets,
backups, deployment identity, and infrastructure-as-code ownership.

## 18. Observability and Operational Model

  ---------------------------------------------------------------------------
  Signal            What it answers   Required fields /     Destination
                                      labels                
  ----------------- ----------------- --------------------- -----------------
  Logs              What happened?    timestamp, severity,  `{{SINK}}`
                                      service, version,     
                                      run/correlation ID,   
                                      outcome               

  Metrics           How often / how   bounded-cardinality   `{{SINK}}`
                    much?             dimensions            

  Traces            Where was time    trace/span IDs,       `{{SINK}}`
                    spent?            dependency calls      

  Audit events      Who did what?     actor, action,        `{{SINK}}`
                                      target, decision,     
                                      result                
  ---------------------------------------------------------------------------

Define dashboard links, alert thresholds, severity, notification
routing, health checks, on-call ownership, and runbooks. Never use
secrets, raw PII, or unbounded user input as metric labels.

## 19. Testing and Verification Strategy

  --------------------------------------------------------------------------
  Level          Scope          Tools          Entry criteria Exit criteria
  -------------- -------------- -------------- -------------- --------------
  Unit           Domain / pure  `{{TOOLS}}`    `{{ENTRY}}`    `{{EXIT}}`
                 logic                                        

  Integration    DB / APIs /    `{{TOOLS}}`    `{{ENTRY}}`    `{{EXIT}}`
                 devices                                      

  Contract       API / events / `{{TOOLS}}`    `{{ENTRY}}`    `{{EXIT}}`
                 MCP schemas                                  

  End-to-end     Critical       `{{TOOLS}}`    `{{ENTRY}}`    `{{EXIT}}`
                 workflows                                    

  Performance    Load / stress  `{{TOOLS}}`    `{{ENTRY}}`    `{{EXIT}}`
                 / soak                                       

  Security       SAST /         `{{TOOLS}}`    `{{ENTRY}}`    `{{EXIT}}`
                 dependency /                                 
                 secrets / DAST                               

  Resilience     Failure /      `{{TOOLS}}`    `{{ENTRY}}`    `{{EXIT}}`
                 recovery                                     

  AI evaluation  Quality /      `{{TOOLS}}`    `{{ENTRY}}`    `{{EXIT}}`
                 safety / tool                                
                 use                                          
  --------------------------------------------------------------------------

## 20. Architecture Decisions (ADR Index)

  ------------------------------------------------------------------------------
  ADR ID      Title         Status       Date         Decision      Link
                                                      owner         
  ----------- ------------- ------------ ------------ ------------- ------------
  ADR-001     `{{TITLE}}`   Proposed /   `{{DATE}}`   `{{OWNER}}`   `{{LINK}}`
                            Accepted /                              
                            Rejected /                              
                            Superseded                              

  ------------------------------------------------------------------------------

### ADR minimum structure

Each significant ADR MUST contain: 1. Context and problem. 2. Decision
drivers and constraints. 3. Options considered. 4. Decision and
rationale. 5. Positive and negative consequences. 6. Security /
operational / cost implications. 7. Status, owner, date, and superseding
ADR if any.

## 21. Risks, Technical Debt and Open Questions

  ------------------------------------------------------------------------------------------------------
  ID       Item         Type       Likelihood    Impact        Mitigation /   Owner         Due
                                                               next action                  
  -------- ------------ ---------- ------------- ------------- -------------- ------------- ------------
  R-001    `{{ITEM}}`   Risk /     `{{L/M/H}}`   `{{L/M/H}}`   `{{ACTION}}`   `{{OWNER}}`   `{{DATE}}`
                        Debt /                                                              
                        Question                                                            

  ------------------------------------------------------------------------------------------------------

## 22. Delivery Roadmap and Traceability

  ----------------------------------------------------------------------------------------------------
  Milestone         Deliverable         Dependencies       Owner         Target date  Exit criteria
  ----------------- ------------------- ------------------ ------------- ------------ ----------------
  `{{MILESTONE}}`   `{{DELIVERABLE}}`   `{{DEPENDENCY}}`   `{{OWNER}}`   `{{DATE}}`   `{{CRITERIA}}`

  ----------------------------------------------------------------------------------------------------

## 23. Architecture Review and Approval Gates

-   [ ] Requirements have measurable acceptance criteria.
-   [ ] Current and target architecture are clearly distinguished.
-   [ ] Component, data-flow, runtime, and deployment views are
    accurate.
-   [ ] Interfaces and schemas have owners and versioning.
-   [ ] Security, privacy, and threat model reviewed.
-   [ ] Failure modes, recovery, and operational ownership defined.
-   [ ] Performance, capacity, and cost assumptions have evidence.
-   [ ] Test and AI evaluation plans are measurable.
-   [ ] ADRs and risks are recorded.
-   [ ] Python / MCP / agent-specific controls completed where
    applicable.
-   [ ] Cross-document references resolve.
-   [ ] No unsupported claims or unresolved critical `TBD`s remain.

  ------------------------------------------------------------------------------------------
  Approver       Name           Decision                       Date           Conditions
  -------------- -------------- ------------------------------ -------------- --------------
  Technical      `{{NAME}}`     `{{APPROVE / REJECT}}`         `{{DATE}}`     `{{NOTES}}`
  Owner                                                                       

  Security       `{{NAME}}`     `{{APPROVE / REJECT / N/A}}`   `{{DATE}}`     `{{NOTES}}`

  Operations     `{{NAME}}`     `{{APPROVE / REJECT / N/A}}`   `{{DATE}}`     `{{NOTES}}`

  Business Owner `{{NAME}}`     `{{APPROVE / REJECT}}`         `{{DATE}}`     `{{NOTES}}`
  ------------------------------------------------------------------------------------------

## 24. Documentation Maintenance Policy

Architecture documentation is a living engineering artifact.

-   Architecture-affecting code, configuration, data, security, or
    deployment changes MUST update the relevant documentation in the
    same change / release workflow.
-   Proposed architecture MUST be labelled as proposed until implemented
    and verified.
-   The production architecture record MUST describe what is actually
    deployed, not merely what was intended.
-   Every diagram and supporting artifact MUST be linked from this
    document or its index.
-   Review documentation drift during release and architecture reviews.

------------------------------------------------------------------------

**End of template.** Replace placeholders, remove non-applicable
sections with a reason, and obtain the required approvals.