# Enterprise Production Script & Automation Engineering Standard --- V2.0

> **Purpose:** Specify, design, implement, test, secure, package,
> release, and operate production-grade scripts and automation.\
> **Technology:** Universal by design, with focused standards for Python
> automation, infrastructure / network automation, APIs, MCP tools, and
> AI-agent workflows.

------------------------------------------------------------------------

## Document Control

  Field                                    Value
  ---------------------------------------- ----------------------------------------------
  Project / Script                         `{{NAME}}`
  Document ID                              `{{DOC_ID}}`
  Version                                  `2.0`
  Repository                               `{{URL}}`
  Entry point                              `{{PATH}}`
  Language / runtime                       `{{LANGUAGE / VERSION}}`
  Owner / maintainer                       `{{OWNER}}`
  Execution mode                           `{{CLI / API / SCHEDULED / EVENT / WORKER}}`
  Criticality                              `{{LOW / MEDIUM / HIGH / CRITICAL}}`
  Target environment                       `{{ENVIRONMENT}}`
  Related architecture / deployment docs   `{{LINKS}}`

## 0. Mandatory Engineering Rules

1.  Requirements, inputs, outputs, side effects, and failure behavior
    MUST be defined before implementation.
2.  Code MUST be modular, testable, reviewable, and maintainable.
3.  Configuration MUST be externalized and validated at startup.
4.  Secrets MUST NOT be committed, hard-coded, printed, or returned to
    untrusted callers.
5.  External calls MUST have explicit timeouts, bounded retries, and
    error classification.
6.  State-changing operations MUST be idempotent or protected against
    duplicate execution.
7.  Destructive or high-impact operations MUST have scope checks,
    authorization, and approval safeguards.
8.  Logs MUST be actionable and MUST NOT expose secrets or unnecessary
    sensitive data.
9.  Critical behavior MUST have automated tests and measurable
    acceptance criteria.
10. A script MUST NOT be called production-ready until operational
    ownership, monitoring, runbook, recovery, and release evidence
    exist.
11. AI coding agents MUST inspect the existing repository conventions
    before changing code.
12. Unknown details MUST be marked `TBD`; never fabricate environment
    values, endpoints, commands, or results.

## 1. Problem Statement and Scope

-   **Business / operational problem:** `{{PROBLEM}}`
-   **Script responsibility:** `{{RESPONSIBILITY}}`
-   **Primary users / callers:** `{{ACTORS}}`
-   **Trigger:** `{{MANUAL / SCHEDULE / API / EVENT}}`
-   **In scope:** `{{SCOPE}}`
-   **Out of scope:** `{{NON_GOALS}}`
-   **Impact of failure:** `{{IMPACT}}`
-   **Expected volume / frequency:** `{{VOLUME}}`

## 2. Requirements and Acceptance Criteria

### 2.1 Functional requirements

  --------------------------------------------------------------------------------------------------
  ID             Requirement                 Priority       Acceptance criteria       Test ID
  -------------- --------------------------- -------------- ------------------------- --------------
  FR-001         `{{THE SCRIPT SHALL...}}`   Must / Should  `{{MEASURABLE RESULT}}`   `{{TEST}}`
                                             / Could                                  

  --------------------------------------------------------------------------------------------------

### 2.2 Non-functional requirements

  Attribute                 Target              Verification
  ------------------------- ------------------- ----------------------
  Execution duration        `{{TARGET}}`        Benchmark
  Throughput / batch size   `{{TARGET}}`        Load test
  Reliability               `{{TARGET}}`        Failure / retry test
  Security                  `{{REQUIREMENT}}`   Security review
  Maintainability           `{{STANDARD}}`      Code review
  Observability             `{{STANDARD}}`      Operational test
  Portability               `{{PLATFORMS}}`     Compatibility test
  Cost / API usage          `{{LIMIT}}`         Usage monitoring

### 2.3 Definition of success

`{{EXACT CONDITIONS THAT MAKE A RUN SUCCESSFUL}}`

## 3. Repository Discovery Before Coding

AI coding agents and contributors MUST inspect the existing project
before implementing:

-   README and project instructions (`AGENTS.md`, `CLAUDE.md`, or
    equivalent).
-   Source layout and entry points.
-   Dependency manifest and lockfile.
-   Existing configuration and environment examples.
-   Unit / integration tests and fixtures.
-   CI workflows, linters, formatters, type checkers, pre-commit hooks.
-   Docker / deployment / scheduler definitions.
-   Logging, metrics, and error-handling conventions.
-   Recent changes and related ADRs.

### Discovery record

  Area                   File / path inspected   Findings
  ---------------------- ----------------------- ---------------
  Project instructions   `{{PATH}}`              `{{FINDING}}`
  Source / entrypoint    `{{PATH}}`              `{{FINDING}}`
  Dependencies           `{{PATH}}`              `{{FINDING}}`
  Tests                  `{{PATH}}`              `{{FINDING}}`
  CI / deployment        `{{PATH}}`              `{{FINDING}}`

Do not introduce a new framework or architectural pattern before
checking whether the repository already has an accepted convention.

## 4. Inputs, Outputs and Side Effects

### 4.1 Input contract

  -------------------------------------------------------------------------------
  Input         Source         Type /       Required    Validation   Sensitive?
                               schema                                
  ------------- -------------- ------------ ----------- ------------ ------------
  `{{INPUT}}`   `{{SOURCE}}`   `{{TYPE}}`   Yes / No    `{{RULE}}`   Yes / No

  -------------------------------------------------------------------------------

### 4.2 Output contract

  ---------------------------------------------------------------------------------
  Output         Destination         Schema /       Consumer         Validation
                                     format                          
  -------------- ------------------- -------------- ---------------- --------------
  `{{OUTPUT}}`   `{{DESTINATION}}`   `{{FORMAT}}`   `{{CONSUMER}}`   `{{RULE}}`

  ---------------------------------------------------------------------------------

### 4.3 Side-effect inventory

  ----------------------------------------------------------------------------------------------------
  Side effect                            Target         Risk           Authorization    Verification /
                                                                                        compensation
  -------------------------------------- -------------- -------------- ---------------- --------------
  `{{CHANGE / WRITE / DELETE / SEND}}`   `{{TARGET}}`   `{{LEVEL}}`    `{{APPROVAL}}`   `{{METHOD}}`

  ----------------------------------------------------------------------------------------------------

## 5. Workflow and State Model

### 5.1 Workflow

``` mermaid
flowchart TD
    A[Start / Trigger] --> B[Load and Validate Configuration]
    B --> C[Validate Identity, Scope and Inputs]
    C --> D{Pre-checks Pass?}
    D -- No --> E[Record Failure and Exit Safely]
    D -- Yes --> F[Execute Idempotent Work Units]
    F --> G[Validate Each Result]
    G --> H{Recoverable Error?}
    H -- Yes --> I[Bounded Retry / Checkpoint]
    I --> F
    H -- No --> J[Record Failed Item / Stop by Policy]
    G --> K[Persist / Publish Results]
    K --> L[Reconcile Counts and State]
    L --> M[Emit Run Summary and Exit]
```

Replace this with the actual process and include compensation paths for
side effects.

### 5.2 Execution state

  State       Meaning         Allowed next states
  ----------- --------------- ------------------------------
  Pending     `{{MEANING}}`   Running / Cancelled
  Running     `{{MEANING}}`   Succeeded / Partial / Failed
  Partial     `{{MEANING}}`   Resumed / Failed / Succeeded
  Succeeded   `{{MEANING}}`   Terminal
  Failed      `{{MEANING}}`   Retryable / Terminal
  Cancelled   `{{MEANING}}`   Terminal / Resumable

## 6. Architecture and Project Structure

### 6.1 Design principles

-   Separate domain / business logic from I/O and vendor-specific
    clients.
-   Keep entry points thin; orchestration belongs in application
    services.
-   Use explicit interfaces and typed data contracts where practical.
-   Inject external dependencies to enable deterministic tests.
-   Avoid global mutable state and hidden side effects.
-   Keep pure transformations separate from network, file, and database
    operations.
-   Centralize configuration, logging, and error classification.
-   Keep each module cohesive and avoid circular dependencies.

### 6.2 Suggested Python layout

Adapt to actual complexity; do not create empty layers for a small
script.

``` text
project/
├── src/
│   └── package_name/
│       ├── __init__.py
│       ├── __main__.py
│       ├── cli.py
│       ├── config.py
│       ├── models.py
│       ├── validators.py
│       ├── exceptions.py
│       ├── logging_config.py
│       ├── services/
│       ├── clients/
│       ├── repositories/
│       └── utils/
├── tests/
│   ├── unit/
│   ├── integration/
│   ├── contract/
│   └── fixtures/
├── docs/
├── scripts/
├── .env.example
├── pyproject.toml
├── [lockfile]
└── README.md
```

### 6.3 Module responsibility matrix

  -----------------------------------------------------------------------
  Module                  Responsibility          Dependency direction
  ----------------------- ----------------------- -----------------------
  `cli.py` / entry point  Parse arguments and     Calls application layer
                          start application       

  `config.py`             Load and validate       Used by composition
                          settings                root

  `models.py`             Typed domain /          Low-level / shared
                          transport structures    

  `validators.py`         Validate input and      Called by services
                          external responses      

  `services/`             Business workflows      Uses interfaces /
                                                  clients

  `clients/`              API, SSH, DB, cloud,    External boundary
                          MCP adapters            

  `repositories/`         Persistence operations  Storage boundary

  `exceptions.py`         Explicit error taxonomy Shared

  `logging_config.py`     Logging setup and       Shared infrastructure
                          redaction               
  -----------------------------------------------------------------------

## 7. Configuration and Environment Management

  -------------------------------------------------------------------------------------
  Key             Purpose         Type         Default         Required    Validation
  --------------- --------------- ------------ --------------- ----------- ------------
  `{{SETTING}}`   `{{PURPOSE}}`   `{{TYPE}}`   `{{DEFAULT}}`   Yes / No    `{{RULE}}`

  -------------------------------------------------------------------------------------

Requirements:

-   Load configuration from approved environment variables, config
    files, or secret managers.
-   Validate required values, types, ranges, URLs, paths, and mutually
    dependent settings before doing work.
-   Define precedence when multiple sources exist.
-   Use separate settings for development, test, staging, and
    production.
-   Provide `.env.example` with placeholder values only.
-   Fail fast with a safe, actionable error when required configuration
    is invalid.
-   Do not log secret values.

## 8. Input Validation and Data Quality

-   Validate schema, type, size, range, encoding, and allowed values.
-   Normalize only according to documented rules.
-   Reject path traversal, command injection, SQL injection, and unsafe
    deserialization.
-   Validate external responses before consuming them.
-   Handle missing, duplicate, malformed, stale, and out-of-order data.
-   Define quarantine / skip / fail behavior for invalid records.
-   Reconcile input, processed, succeeded, failed, and skipped counts.

  -----------------------------------------------------------------------
  Field / input     Validation rule   Invalid behavior  Evidence / test
  ----------------- ----------------- ----------------- -----------------
  `{{FIELD}}`       `{{RULE}}`        Reject /          `{{TEST_ID}}`
                                      quarantine / skip 

  -----------------------------------------------------------------------

## 9. Error Taxonomy and Resilience

### 9.1 Error categories

  -----------------------------------------------------------------------
  Category          Example           Retry?            Handling
  ----------------- ----------------- ----------------- -----------------
  Validation        Invalid / missing No                Reject with safe
                    input                               message

  Authentication    Invalid / expired Usually no        Stop and alert
                    credentials                         owner

  Authorization     Insufficient      No                Deny and audit
                    permission                          

  Rate limit        HTTP 429 / quota  Bounded           Respect retry
                                                        guidance

  Transient network Timeout /         Bounded           Backoff with
                    connection reset                    jitter

  Permanent remote  Non-retryable 4xx No                Record and stop /
  error                                                 skip

  Data integrity    Duplicate /       Not blindly       Quarantine /
                    mismatch                            reconcile

  Internal defect   Unexpected        No blind retry    Log safely and
                    exception                           alert
  -----------------------------------------------------------------------

### 9.2 Retry policy

-   Maximum attempts: `{{N}}`
-   Backoff: `{{FIXED / EXPONENTIAL}}`
-   Jitter: `{{YES / NO}}`
-   Retryable error list: `{{LIST}}`
-   Per-attempt timeout: `{{DURATION}}`
-   Overall execution deadline: `{{DURATION}}`
-   Retry budget / rate limit: `{{LIMIT}}`

Retries MUST be bounded. Do not automatically retry a non-idempotent
write unless deduplication or idempotency protection exists.

### 9.3 Partial failure policy

-   Batch behavior: `{{FAIL FAST / CONTINUE / THRESHOLD}}`
-   Maximum tolerated failures: `{{N / PERCENTAGE}}`
-   Failed item storage: `{{LOCATION}}`
-   Resume / replay behavior: `{{METHOD}}`
-   Manual recovery: `{{RUNBOOK}}`

## 10. Idempotency, Concurrency and Checkpointing

-   Idempotency key / natural key: `{{KEY}}`
-   Duplicate detection: `{{METHOD}}`
-   Locking / lease: `{{METHOD}}`
-   Maximum concurrent runs: `{{N}}`
-   Overlap behavior: `{{REJECT / QUEUE / ALLOW}}`
-   Checkpoint granularity: `{{ITEM / BATCH / PHASE}}`
-   Resume semantics: `{{METHOD}}`
-   Stale lock recovery: `{{METHOD}}`

For state-changing automation, repeated execution MUST NOT create
unintended duplicate changes.

## 11. Logging, Metrics and Audit

### 11.1 Structured log schema

  Field                        Purpose
  ---------------------------- -------------------------------
  timestamp                    UTC or documented timezone
  level                        Severity
  service / script / version   Runtime identity
  environment                  Execution environment
  run_id                       Unique execution identifier
  correlation_id               Cross-system trace identifier
  operation / target           Safe operation context
  duration_ms                  Timing
  outcome / error_code         Result classification

### 11.2 Required events

  Event                Level     Required context
  -------------------- --------- ------------------------------------
  Run started          INFO      run_id, version, trigger
  Pre-check complete   INFO      scope, validation outcome
  Work unit complete   INFO      item / batch ID, duration, outcome
  Retry                WARNING   error category, attempt, delay
  Item failed          ERROR     safe target reference, error code
  Run summary          INFO      totals, duration, final status

### 11.3 Metrics

-   Runs started / completed / failed.
-   Success / failure / skipped counts.
-   Duration and throughput.
-   Retry count and timeout count.
-   API rate limit / quota consumption.
-   Queue depth / backlog where applicable.
-   Cost / token usage for AI workloads.

Never put secrets, raw PII, or high-cardinality arbitrary values in
metrics labels.

## 12. Security and Secure Coding

### 12.1 Baseline controls

-   Least-privilege service identity.
-   Secret manager / secure credential store.
-   TLS for network traffic.
-   Explicit connection and read timeouts.
-   Input validation and output encoding.
-   Parameterized database queries.
-   Safe subprocess execution; avoid shell interpolation of untrusted
    values.
-   Dependency pinning / lockfile and vulnerability scanning.
-   Restricted filesystem permissions and temporary-file cleanup.
-   Log redaction and access control.
-   Audit logging for sensitive actions.
-   Defined credential rotation and revocation.

### 12.2 High-impact automation controls

-   [ ] Explicit target allowlist / scope validation.
-   [ ] Dry-run / preview mode.
-   [ ] Maximum target count / batch size.
-   [ ] Concurrency and rate limits.
-   [ ] Pre-change snapshot / backup.
-   [ ] Approval gate for destructive actions.
-   [ ] Post-change verification.
-   [ ] Emergency stop / cancellation.
-   [ ] Rollback / compensation plan.
-   [ ] Run-level and item-level audit evidence.

## 13. Python Engineering Standard

Complete when the implementation uses Python.

### 13.1 Runtime and tooling

  Concern              Standard / selected tool
  -------------------- ---------------------------------------
  Python version       `{{SUPPORTED VERSION RANGE}}`
  Package management   `{{uv / pip-tools / poetry / other}}`
  Dependency lock      `{{LOCKFILE}}`
  Formatting / lint    `{{ruff / black / other}}`
  Type checking        `{{mypy / pyright / other}}`
  Testing              `{{pytest / unittest}}`
  Security scan        `{{bandit / pip-audit / other}}`
  Pre-commit           `{{TOOL / CONFIG}}`
  Build / package      `{{WHEEL / CONTAINER / EXECUTABLE}}`

### 13.2 Python coding requirements

-   Follow the team's agreed style guide; PEP 8 is the default baseline.
-   Add type hints to public functions and important boundaries.
-   Use context managers for files, DB sessions, SSH clients, and HTTP
    clients.
-   Use `pathlib` for filesystem paths where suitable.
-   Use `logging` / approved structured logger instead of `print` for
    operational output.
-   Use explicit encodings for text files and handle decoding failures
    intentionally.
-   Use `argparse`, Click, Typer, or the project's established CLI
    framework.
-   Avoid broad `except Exception` unless at a deliberate process
    boundary with safe logging and correct exit behavior.
-   Do not swallow exceptions or return success after a failed
    operation.
-   Close resources reliably and handle cancellation.
-   Keep business logic testable without live network or production
    credentials.

### 13.3 Python HTTP / SSH / database client rules

-   Explicit connect and read timeouts.
-   TLS verification enabled by default.
-   Bounded retries for safe operations only.
-   Session / connection reuse where appropriate.
-   Explicit pagination and response-size limits.
-   Validate response status and schema.
-   Close sessions and connections deterministically.
-   Do not disable host-key or certificate verification to bypass errors
    in production.
-   For SSH / device automation, verify host identity and use approved
    credentials and command allowlists.

## 14. API and Infrastructure Automation

### 14.1 API integration contract

  Item                     Value
  ------------------------ -----------------
  Base URL / API version   `{{REFERENCE}}`
  Authentication           `{{METHOD}}`
  Scopes / permissions     `{{SCOPES}}`
  Timeout / deadline       `{{DURATION}}`
  Rate limit               `{{LIMIT}}`
  Pagination               `{{METHOD}}`
  Retryable statuses       `{{LIST}}`
  Idempotency strategy     `{{METHOD}}`
  Response validation      `{{SCHEMA}}`

### 14.2 Infrastructure / network automation

-   Inventory source and target allowlist: `{{SOURCE}}`
-   Pre-checks: reachability, identity, version, state, authorization.
-   Command / change plan: `{{REFERENCE}}`
-   Prompt / session handling: `{{METHOD}}`
-   Command timeout and pagination: `{{POLICY}}`
-   Backup / pre-change snapshot: `{{METHOD}}`
-   Batch / concurrency control: `{{LIMIT}}`
-   Post-checks: expected state and health.
-   Partial failure strategy: `{{POLICY}}`
-   Rollback / compensation: `{{METHOD}}`

A command being sent is not proof of success. Validate the actual
resulting state.

## 15. MCP Server and Tool Engineering

Complete when exposing MCP capabilities.

### 15.1 Tool contract

  ----------------------------------------------------------------------------------------------------
  Tool              Purpose         Input schema   Output schema  Permission    Side effect
  ----------------- --------------- -------------- -------------- ------------- ----------------------
  `{{TOOL_NAME}}`   `{{PURPOSE}}`   `{{SCHEMA}}`   `{{SCHEMA}}`   `{{SCOPE}}`   `{{NONE / DETAILS}}`

  ----------------------------------------------------------------------------------------------------

Each tool MUST: - Have a narrow, unambiguous purpose. - Validate
arguments server-side against a strict schema. - Authenticate and
authorize each protected operation. - Enforce timeouts, payload limits,
concurrency, and quotas. - Return structured, safe, actionable errors. -
Avoid leaking credentials, stack traces, internal hostnames, or
sensitive records. - Clearly distinguish read-only, mutating, and
destructive behavior. - Audit consequential operations. - Require
explicit confirmation for destructive / irreversible actions.

### 15.2 MCP server runtime

-   SDK / framework and version: `{{VERSION}}`
-   Transport: `{{STDIO / STREAMABLE HTTP / OTHER SUPPORTED}}`
-   Client compatibility matrix: `{{CLIENTS}}`
-   Authentication / authorization: `{{METHOD}}`
-   Health / readiness: `{{METHOD}}`
-   Session / state handling: `{{METHOD}}`
-   Tool registry and schema versioning: `{{METHOD}}`
-   Logging / audit: `{{METHOD}}`

## 16. AI Agent / LLM Engineering

Complete when a script calls an LLM or participates in an agent
workflow.

### 16.1 Model and prompt configuration

  Setting                             Value
  ----------------------------------- ----------------
  Provider / endpoint                 `{{PROVIDER}}`
  Model ID / pinned version           `{{MODEL}}`
  Prompt / policy version             `{{VERSION}}`
  Temperature / generation settings   `{{SETTINGS}}`
  Token budget                        `{{LIMIT}}`
  Timeout                             `{{LIMIT}}`
  Cost budget                         `{{LIMIT}}`
  Fallback behavior                   `{{POLICY}}`

### 16.2 Agent tool safety

-   Tool allowlist and per-tool scopes: `{{LIST}}`
-   Maximum agent steps / iterations: `{{LIMIT}}`
-   Human approval conditions: `{{RULES}}`
-   Untrusted prompt / retrieval content handling: `{{RULES}}`
-   Tool argument validation: `{{METHOD}}`
-   Tool output validation: `{{METHOD}}`
-   Memory / context retention: `{{POLICY}}`
-   Stop conditions and escalation: `{{POLICY}}`

Prompts are not an authorization boundary. Enforce permissions and
safety rules in application code and the tool server.

### 16.3 AI evaluation

  --------------------------------------------------------------------------------------
  Test set        Scenario       Metric         Threshold                 Result
  --------------- -------------- -------------- ------------------------- --------------
  `{{DATASET}}`   Task success   `{{METRIC}}`   `{{TARGET}}`              `{{RESULT}}`

  `{{DATASET}}`   Tool           `{{METRIC}}`   `{{TARGET}}`              `{{RESULT}}`
                  correctness                                             

  `{{DATASET}}`   Prompt         `{{METRIC}}`   `{{TARGET}}`              `{{RESULT}}`
                  injection                                               

  `{{DATASET}}`   Data leakage   `{{METRIC}}`   `0 critical violations`   `{{RESULT}}`
  --------------------------------------------------------------------------------------

## 17. Testing Strategy and Quality Gates

  -----------------------------------------------------------------------
  Test type         Scope             Tool              Required evidence
  ----------------- ----------------- ----------------- -----------------
  Unit              Pure logic /      `{{TOOL}}`        `{{REPORT}}`
                    validators                          

  Integration       API / DB / SSH /  `{{TOOL}}`        `{{REPORT}}`
                    filesystem                          

  Contract          External API /    `{{TOOL}}`        `{{REPORT}}`
                    MCP schemas                         

  End-to-end        Critical workflow `{{TOOL}}`        `{{REPORT}}`

  Negative /        Invalid and       `{{TOOL}}`        `{{REPORT}}`
  boundary          malicious input                     

  Resilience        Timeout / retry / `{{TOOL}}`        `{{REPORT}}`
                    partial failure                     

  Performance       Volume /          `{{TOOL}}`        `{{REPORT}}`
                    concurrency                         

  Security          Secrets /         `{{TOOL}}`        `{{REPORT}}`
                    dependency /                        
                    permissions                         

  AI evaluation     Quality / tool    `{{TOOL}}`        `{{REPORT}}`
                    safety                              
  -----------------------------------------------------------------------

### 17.1 Mandatory scenarios

-   Valid input and expected output.
-   Missing, malformed, oversized, and boundary input.
-   Invalid credentials and insufficient permissions.
-   Timeout, rate limit, transient and permanent remote failures.
-   Duplicate / concurrent execution.
-   Partial batch failure and resume.
-   Unexpected response schema or encoding.
-   Secret / PII redaction in logs and errors.
-   Dry-run performs no unintended mutation.
-   Destructive operation is blocked without required approval.
-   Cancellation and cleanup leave the system in a known state.

### 17.2 CI quality gates

Select project-appropriate checks; do not claim checks are enabled until
the pipeline proves it.

-   [ ] Formatter / linter.
-   [ ] Type checker.
-   [ ] Unit and integration tests.
-   [ ] Coverage threshold: `{{TARGET / JUSTIFICATION}}`.
-   [ ] Dependency vulnerability scan.
-   [ ] Static security scan.
-   [ ] Secret scan.
-   [ ] Build / package validation.
-   [ ] Container scan where applicable.
-   [ ] Documentation / schema validation.

## 18. Performance, Capacity and Cost

  Dimension                        Expected          Peak   Limit / alert
  --------------------------- ------------- ------------- ---------------
  Records / targets per run         `{{N}}`       `{{N}}`     `{{LIMIT}}`
  Requests per minute               `{{N}}`       `{{N}}`     `{{LIMIT}}`
  Execution duration             `{{TIME}}`    `{{TIME}}`     `{{LIMIT}}`
  Memory / CPU                  `{{VALUE}}`   `{{VALUE}}`     `{{LIMIT}}`
  LLM tokens / run                  `{{N}}`       `{{N}}`     `{{LIMIT}}`
  Cost per run                  `{{VALUE}}`   `{{VALUE}}`     `{{LIMIT}}`

Record benchmark environment, dataset size, test method, and result.

## 19. Packaging, Release and Supply Chain

-   Artifact type: `{{SOURCE / WHEEL / EXECUTABLE / CONTAINER}}`
-   Build command / pipeline: `{{REFERENCE}}`
-   Versioning scheme: `{{SEMVER / OTHER}}`
-   Dependency lock: `{{FILE}}`
-   SBOM / provenance: `{{REFERENCE}}`
-   Artifact hash / signature: `{{REFERENCE}}`
-   Runtime / OS compatibility: `{{MATRIX}}`
-   Upgrade / downgrade method: `{{METHOD}}`
-   Release notes / changelog: `{{PATH}}`

Build once and promote the same verified artifact across environments
wherever possible.

## 20. Scheduling and Runtime Operations

  Operational setting        Value
  -------------------------- -----------------------------------
  Trigger / scheduler        `{{CRON / EVENT / MANUAL / API}}`
  Schedule expression        `{{EXPRESSION}}`
  Timezone                   `{{TIMEZONE}}`
  Execution identity         `{{SERVICE ACCOUNT}}`
  Working directory          `{{PATH}}`
  Runtime / environment      `{{DETAILS}}`
  Maximum duration           `{{TIMEOUT}}`
  Overlap policy             `{{PREVENT / QUEUE / ALLOW}}`
  Lock / deduplication       `{{METHOD}}`
  Output / log destination   `{{LOCATION}}`
  Failure notification       `{{CHANNEL}}`
  Retention / cleanup        `{{POLICY}}`

## 21. Runbook and Recovery Procedure

### Pre-run

1.  Confirm approval and target scope.
2.  Validate environment, identity, dependencies, and connectivity.
3.  Confirm required backup / snapshot.
4.  Run dry-run / preview where supported.
5.  Record run ID and operator.

### Execution

1.  Execute the approved entry point / pipeline.
2.  Monitor progress, logs, and key metrics.
3.  Stop safely if a predefined threshold is crossed.
4.  Record partial failures and recovery decisions.

### Post-run

1.  Validate output and actual target state.
2.  Reconcile processed / succeeded / failed / skipped counts.
3.  Verify no unintended side effects.
4.  Publish results and evidence.
5.  Close the run record and notify stakeholders.

### Recovery

-   Stop / cancel: `{{METHOD}}`
-   Resume from checkpoint: `{{METHOD}}`
-   Retry failed items: `{{METHOD}}`
-   Rollback / compensation: `{{METHOD}}`
-   Escalation: `{{OWNER / CHANNEL}}`

## 22. Code Review Checklist

-   [ ] Requirements and acceptance criteria are implemented.
-   [ ] Repository conventions and architecture are followed.
-   [ ] Modules and functions have clear responsibilities.
-   [ ] Inputs and external responses are validated.
-   [ ] Error taxonomy and exit codes are consistent.
-   [ ] Timeouts and bounded retries are applied.
-   [ ] Side effects are idempotent or duplicate-protected.
-   [ ] Secrets and sensitive data are protected.
-   [ ] Permissions and target scope are least-privilege.
-   [ ] Logs, metrics, and audit events are actionable.
-   [ ] Tests cover positive, negative, boundary, and failure paths.
-   [ ] Dependencies are locked and scanned.
-   [ ] Documentation and runbooks are updated.
-   [ ] Destructive actions have safeguards and approval.

## 23. Production Readiness and Release Approval

### Engineering

-   [ ] Code review approved.
-   [ ] CI quality gates passed.
-   [ ] Tests and required coverage passed.
-   [ ] Build and dependency lock reproducible.
-   [ ] Configuration validated.
-   [ ] No hard-coded secrets or environment-specific assumptions.

### Reliability

-   [ ] Timeouts, retries, idempotency, and recovery tested.
-   [ ] Partial failures and duplicate runs handled.
-   [ ] Health / completion status available.
-   [ ] Stop and resume behavior documented.

### Security

-   [ ] Least-privilege identity confirmed.
-   [ ] Secret handling and rotation defined.
-   [ ] Inputs and tool arguments validated.
-   [ ] Logs redacted.
-   [ ] High-impact actions gated by approval.

### Operations

-   [ ] Named owner and support path.
-   [ ] Runbook and rollback instructions reviewed.
-   [ ] Monitoring and alerts configured.
-   [ ] Scheduler / runtime settings validated.
-   [ ] Backup / checkpoint / recovery requirements met.

### Approval

  --------------------------------------------------------------------------
  Role           Name           Decision       Date           Evidence /
                                                              comments
  -------------- -------------- -------------- -------------- --------------
  Developer      `{{NAME}}`     Submitted      `{{DATE}}`     `{{LINK}}`

  Reviewer       `{{NAME}}`     Approved /     `{{DATE}}`     `{{LINK}}`
                                Changes                       
                                required                      

  Technical      `{{NAME}}`     Approved /     `{{DATE}}`     `{{LINK}}`
  Owner                         Rejected                      

  Security /     `{{NAME}}`     Approved / N/A `{{DATE}}`     `{{LINK}}`
  Operations                                                  
  --------------------------------------------------------------------------

## 24. Execution Record

  -------------------------------------------------------------------------------------------------------
  Run ID         Timestamp    Trigger /         Processed    Success     Failed     Duration Evidence
                              operator                                                       
  -------------- ------------ --------------- ----------- ---------- ---------- ------------ ------------
  `{{RUN_ID}}`   `{{TIME}}`   `{{TRIGGER}}`       `{{N}}`    `{{N}}`    `{{N}}`   `{{TIME}}` `{{LINK}}`

  -------------------------------------------------------------------------------------------------------

## 25. Known Issues and Technical Debt

  ----------------------------------------------------------------------------------------
  ID          Issue / debt    Impact         Workaround         Owner         Due date
  ----------- --------------- -------------- ------------------ ------------- ------------
  `{{ID}}`    `{{DETAILS}}`   `{{IMPACT}}`   `{{WORKAROUND}}`   `{{OWNER}}`   `{{DATE}}`

  ----------------------------------------------------------------------------------------

## 26. Definition of Done

A script is production-ready only when:

1.  Its behavior, contracts, side effects, and acceptance criteria are
    documented.
2.  It follows repository and architecture conventions.
3.  Security, identity, authorization, and secret handling are enforced.
4.  Error handling, deadlines, retries, idempotency, and recovery are
    tested.
5.  Logs, metrics, and audit trails support diagnosis.
6.  Automated tests and CI quality gates pass.
7.  Packaging, configuration, and release are reproducible.
8.  Operational runbook, monitoring, and named ownership exist.
9.  Production scope and execution are approved.
10. Evidence and final sign-off are recorded.

------------------------------------------------------------------------

**End of template.** Replace all `{{PLACEHOLDERS}}`, remove
non-applicable sections with a reason, and do not mark a control
complete without evidence.