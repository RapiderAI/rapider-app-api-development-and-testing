<!-- Rapider Official App SOW & Specification | App #103: API Development & Testing (api-testing) | Domain: DEV -->

# #103 API Development & Testing (`api-testing`) — Scope of Work (SOW)

- **App Number & Slug:** `#103` / `103-api-development-and-testing`
- **Proposed Rapider App Key:** `api-testing`
- **Suite / Domain Key:** `DEV` (Software Engineering & DevSecOps Suite — `Dev*` Canonical Prefix)
- **Representative Product (`P1`):** Postman
- **Combined Feature Catalog Reference:** [../combined-features/103-api-development-and-testing-features.md](../combined-features/103-api-development-and-testing-features.md)

---

## 1. Executive Outcome & Target Audience

`api-testing` delivers a Design-First OpenAPI/AsyncAPI Contract Studio, Git-Native Multi-Protocol Request Workbench, Zero-Secret Vault Environment Manager, Dynamic Mock Server Engine, Automated Contract/OWASP Test Runner, and Synthetic API Monitor natively integrated across the Rapider `DEV` suite. Engineering teams regularly ship breaking API changes that crash mobile/partner integrations, leak bearer tokens inside shared Postman JSON exports, or wait weeks for backend endpoints before frontend work can begin. `api-testing` unifies governed specifications (`DevApiSpec`), chained request collections (`DevApiCollection`, `DevApiRequestItem`), vault-referenced environments (`DevApiEnvironment`), instant mocks (`DevMockServer`), CI contract gates (`DevApiTestRun`), and synthetic health probes (`DevApiMonitor`).

- **SME Fast-Path Defaults:** Developers import an OpenAPI file or cURL command (or browse auto-discovered canonical Rapider suite endpoints), switch across `DEV / STAGING / PROD` environments using safe vault references, spin up a live `DevMockServer` in one click for parallel UI work, and schedule a 5-minute synthetic uptime monitor in under three minutes.
- **Enterprise Progressive Disclosure:** API Platform Architects enforce Spectral style & OWASP security linting, gate breaking contract diffs through Architect Home `WorkItem`s, sync declarative collections bi-directionally with `#101` (`source-control`) Git branches, block `#102` (`ci-cd`) deployments on contract drift or BOLA/idempotency regressions, and feed Canary auto-rollback signals (`dev.api.monitor.breached.v1`) directly into `#102`.
- **Measurable Success Outcomes:**
  - `100%` interception of undeclared breaking API contract changes prior to `PUBLISHED` spec promotion or `#101` PR merge.
  - Zero plaintext API keys, bearer tokens, or OAuth secrets persisted in collection exports, request histories, or Git sync commits.
  - Sub-60-second detection of synthetic endpoint degradation (`5xx`, TLS expiry, P95 latency breach) linked to `#102` Canary rollback and SRE Home `WorkItem`s.
- **Top 6 Global Benchmarks Synthesized:** `P1` Postman, `P2` Kong Insomnia, `P3` Bruno, `P4` SmartBear SwaggerHub & ReadyAPI, `P5` Salesforce MuleSoft Anypoint, and `P6` SAP Integration Suite API Management.

---

## 2. In-Scope, Out-of-Scope & Suite Ownership Boundaries

### In-Scope
1. Design-First OpenAPI `3.0/3.1`, AsyncAPI `3.0`, and GraphQL SDL specification authoring (`DevApiSpec`), Spectral linting, agent/MCP schema readiness checks, and breaking-change approval workflows via Home `WorkItem`s.
2. Multi-protocol request workbench (`HTTP/REST`, `GraphQL`, `gRPC`, `WebSocket`, `SSE`), request-chaining collections (`DevApiCollection`, `DevApiRequestItem`), multi-language snippet generation, and interactive developer portal docs.
3. Scoped variable environments (`DevApiEnvironment`) backed strictly by Platform Secret Vault references (`vaultSecretRef`) and Cloud Run `.run.app` / ingress URL lint checks.
4. Automated collection test runs (`DevApiTestRun`), JSON Schema / OpenAPI contract drift verification, idempotency/concurrency race checks, and OWASP API Top-10 negative tests.
5. Spec-driven mock servers with chaos/latency injection (`DevMockServer`) and scheduled multi-step synthetic uptime/TLS monitors (`DevApiMonitor`).

### Out-of-Scope
1. Git repository hosting, source code diff reviews, and branch rulesets — owned by `#101 Source Code Hosting & Version Control` (`source-control`), synced bi-directionally via `API-004`.
2. Container builds, general unit test runners, and Kubernetes/Cloud Run deployment rollouts — owned by `#102 Continuous Integration / Deployment (CI/CD)` (`ci-cd`).
3. Production API Gateway runtime proxy routing and enterprise customer billing metering — handled by cloud infrastructure / `FIN` (`billing`, `subscriptions`).
4. Agile engineering bug backlog management — owned by `APM` (`apm`: `ApmIssue`).

### Cross-Suite Ownership & Integration Contract

| Domain / App | Owns (Single Source of Truth) | Integration Contract with `api-testing` (`#103`) |
| :--- | :--- | :--- |
| **`api-testing` (`#103`)** | `DevApiSpec`, `DevApiCollection`, `DevApiRequestItem`, `DevApiEnvironment`, `DevMockServer`, `DevApiTestRun`, `DevApiMonitor` | Publishes contract test results, breaking-change alerts, and synthetic monitor health signals. |
| **`#101` Source Control (`source-control`)** | `DevRepository`, `DevPullRequest`, `DevSecurityAdvisory` | Syncs declarative specs/collections with Git branches; posts `dev.api.test_run.completed.v1` PR status checks and OWASP API findings. |
| **`#102` CI/CD (`ci-cd`)** | `DevPipelineRun`, `DevDeploymentRecord` | Executes headless `DevApiTestRun` gates during `STAGING` pipelines; consumes `dev.api.monitor.breached.v1` to trigger Canary auto-rollback. |
| **`APM` (`apm`) & `SUP` (`support`)** | `ApmProject`, `ApmIssue`, `SupTicket` | Attaches credential-redacted request/response snapshots (`API-028`) to `ApmIssue` defect tickets; links `DevApiMonitor` outages to incident workflows. |
| **`#096` BI Dashboards (`bi-dashboards`)** | `DatDashboard`, `DatMetricDefinition` | Exports `Decimal128` API availability `%`, P95 latency, and contract coverage metrics for engineering leadership scorecards. |

---

## 3. Primary Web Pages & Sidebar Navigation Architecture (12 Pages)

All visible sidebar sections enforce **`>= 3` visible items (`displayOnMenu: true`)**, while detail views, full-screen request workbenches, and drawers set `displayOnMenu: false`.

| # | Route | Page Title | Sidebar Section | Menu Visible | Key Components & UX |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `api-hub` | API Quality & SLA Cockpit | `Design & Collections` | `true` (Order 1) | Contract coverage `%`, synthetic uptime (`Decimal128`), P95 latency ribbon, breaking-change `WorkItem` banner, `#activeFilterTagsBar`. |
| 2 | `api-specs` | API Specifications | `Design & Collections` | `true` (Order 2) | `findSWR` catalog of `DevApiSpec`s (`OPENAPI_3_1`, `ASYNCAPI_3`, `GRAPHQL_SDL`), lint score, agent-readiness badge, clickable spec name, icon+text `Edit`, icon-only `Delete`. |
| 3 | `api-collections` | Request Collections | `Design & Collections` | `true` (Order 3) | `DevApiCollection` directory with `#101` Git sync status, request count, `Run Suite` trigger, `#activeFilterTagsBar` + `Clear all`, clickable collection name, icon+text `Edit`, icon-only `Delete`. |
| 4 | `developer-portal` | Interactive API Portal | `Design & Collections` | `true` (Order 4) | Searchable human + AI-agent documentation portal across `PUBLISHED` specs and canonical Rapider suite APIs with multi-language code snippets. |
| 5 | `api-environments` | Environments & Vault Bindings | `Testing & Mocking` | `true` (Order 5) | `DevApiEnvironment` manager (`LOCAL`, `DEV`, `STAGING`, `PROD`), variable table with `vaultSecretRef` badges (zero plaintext secrets), and `.run.app` / SSL URL lint status. |
| 6 | `mock-servers` | Dynamic Mock Servers | `Testing & Mocking` | `true` (Order 6) | `DevMockServer` fleet table showing live mock URL, bound `DevApiSpec`, chaos/latency injection rules (`429/503`), and live request call inspector count. |
| 7 | `api-test-runs` | Contract & Security Test Runs | `Testing & Mocking` | `true` (Order 7) | `DevApiTestRun` execution ledger (`PASSED`, `FAILED_ASSERTION`, `CONTRACT_DRIFT`, `SECURITY_FAIL`), `#102` pipeline links, and `#activeFilterTagsBar`. |
| 8 | `api-monitors` | Synthetic API Monitors | `Governance & Monitoring` | `true` (Order 8) | `DevApiMonitor` health board (`<rapider-kanban>` + synchronized table) across `HEALTHY`, `DEGRADED_LATENCY`, `FAILING_OUTAGE`, `PAUSED`, with TLS expiry countdowns. |
| 9 | `lint-governance` | Spectral & OWASP Rules | `Governance & Monitoring` | `true` (Order 9) | Workspace API style guide rules, OWASP API Top-10 negative test toggles, and breaking-change approval policy rules. |
| 10 | `breaking-changes` | Contract Diff & Reviews | `Governance & Monitoring` | `true` (Order 10) | Breaking vs. non-breaking `DevApiSpec` semantic diff queue linked to Architect Home `WorkItem`s and `#101` pull requests. |
| 11 | `request-workbench` | Multi-Protocol Request Studio | *(Hidden)* | `false` | Split-pane interactive client (`#/request-workbench?collectionId=...&requestId=...`): folder tree, URL/method bar, Params/Headers/Body/Assertions tabs, timing waterfall, AI Test Generator, and `Back to Collections`. |
| 12 | `spec-test-detail` | Spec Editor & Test Run Detail | *(Hidden)* | `false` | OpenAPI YAML/JSON editor + live Spectral lint + Try-It preview (`#/spec-test-detail?id=...`), `DevApiTestRun` per-assertion diff inspector, plus sliding `api-entity-drawer` (`displayOnMenu: false`). |

---

## 4. Canonical Data Models (`Dev*` — 7 Models)

All models strictly omit `projectId`, store zero plaintext secrets or authorization headers, use platform UUID `id` + optimistic `version`, and use `Decimal128` for availability SLAs and latency/assertion precision.

| Model Name | Key Fields & Types | Relationships & External Refs | Invariants & Lifecycle |
| :--- | :--- | :--- | :--- |
| **`DevApiSpec`** | `id: UUID`, `code: string`, `title: string`, `specFormat: enum(OPENAPI_3_1, OPENAPI_3_0, ASYNCAPI_3_0, GRAPHQL_SDL)`, `semver: string`, `specDocumentText: string`, `lintErrorsCount: int`, `lintWarningsCount: int`, `agentReadinessScorePct: Decimal128`, `hasBreakingDiff: boolean`, `gitRepositoryId: UUID?`, `gitFilePath: string?`, `status: enum(DRAFT, IN_REVIEW, PUBLISHED, DEPRECATED)`, `activeWorkItemId: UUID?`, `discussionChannelId: UUID?`, `version: int` | `gitRepositoryId -> DevRepository.id` (`#101`); `activeWorkItemId -> Platform WorkItem.id`; `discussionChannelId -> projectChannelMessage`. | `(code, semver)` unique. Cannot transition to `PUBLISHED` when `lintErrorsCount > 0` or when `hasBreakingDiff === true` without Architect approval via guarded command. |
| **`DevApiCollection`** | `id: UUID`, `code: string`, `name: string`, `description: string`, `linkedSpecId: UUID?`, `gitRepositoryId: UUID?`, `gitDirectoryPath: string?`, `defaultEnvironmentId: UUID?`, `folderTreeJson: object[]`, `requestCount: int`, `discussionChannelId: UUID?`, `ownerUserId: UUID`, `version: int` | `linkedSpecId -> DevApiSpec.id`; `gitRepositoryId -> DevRepository.id` (`#101`); `defaultEnvironmentId -> DevApiEnvironment.id`. | Deleting a collection soft-deletes child `DevApiRequestItem`s and pauses bound `DevApiMonitor`s atomically. |
| **`DevApiRequestItem`** | `id: UUID`, `collectionId: UUID`, `folderPath: string`, `sortOrder: int`, `name: string`, `protocol: enum(HTTP_REST, GRAPHQL, GRPC, WEBSOCKET, SSE)`, `httpMethod: enum(GET, POST, PUT, PATCH, DELETE, HEAD, OPTIONS)?`, `urlTemplate: string`, `headersJson: {key, valueTemplate, isRedactedRef}[]`, `bodyPayloadJson: object?`, `extractionsJson: {varName, jsonPath}[]`, `assertionsJson: {type, target, operator, expectedValue}[]`, `checkIdempotencyReplay: boolean`, `version: int` | `collectionId -> DevApiCollection.id`. | **Zero-secret invariant:** `headersJson` and `bodyPayloadJson` reject inline `Bearer eyJ...`, `Basic ...`, or hardcoded API keys—requiring `{{env.varName}}` bindings resolved from `DevApiEnvironment`. |
| **`DevApiEnvironment`** | `id: UUID`, `name: string`, `tier: enum(LOCAL, DEV, STAGING, PRODUCTION)`, `baseUrl: string`, `variablesJson: {key, plainValue, vaultSecretRef, isSecret}[]`, `urlLintWarnings: string[]`, `ownerUserId: UUID`, `version: int` | Referenced by `DevApiCollection`, `DevApiTestRun`, & `DevApiMonitor`. | Whenever `isSecret === true`, `plainValue` MUST be `null` and `vaultSecretRef` MUST reference a valid Platform Secret Vault entry. `baseUrl` rejects RFC1918/link-local metadata targets (`169.254.169.254`) on cloud server-side runners. |
| **`DevMockServer`** | `id: UUID`, `code: string`, `name: string`, `specId: UUID`, `mockPathPrefix: string`, `requireMockToken: boolean`, `simulatedLatencyMs: int`, `chaosFailureRatePct: Decimal128`, `chaosStatusCodes: int[]`, `callsServed24h: int`, `status: enum(ACTIVE, PAUSED)`, `version: int` | `specId -> DevApiSpec.id`. | `chaosFailureRatePct` bounded `0.00..100.00` (`Decimal128`); `mockPathPrefix` unique per workspace. |
| **`DevApiTestRun`** | `id: UUID`, `collectionId: UUID`, `environmentId: UUID`, `specId: UUID?`, `triggerSource: enum(INTERACTIVE, CICD_PIPELINE, PR_CHECK, MONITOR)`, `cicdPipelineRunId: UUID?`, `runMode: enum(FUNCTIONAL_CONTRACT, OWASP_SECURITY, SMOKE_LOAD)`, `status: enum(RUNNING, PASSED, FAILED_ASSERTION, CONTRACT_DRIFT, SECURITY_FAIL, ABORTED)`, `totalRequests: int`, `failedAssertions: int`, `contractDriftItemsJson: object[]`, `p95LatencyMs: Decimal128`, `redactedResultsFileId: UUID?`, `startedAt: datetime`, `completedAt: datetime?`, `idempotencyKey: string` | `collectionId -> DevApiCollection.id`; `environmentId -> DevApiEnvironment.id`; `cicdPipelineRunId -> DevPipelineRun.id` (`#102`); `redactedResultsFileId -> Platform Drive File.id`. | Immutable terminal test ledger. All captured request/response headers in `redactedResultsFileId` scrub `Authorization`, `Cookie`, `Set-Cookie`, and `X-Api-Key`. `SMOKE_LOAD` mode is blocked unless `baseUrl` belongs to a verified workspace domain. |
| **`DevApiMonitor`** | `id: UUID`, `name: string`, `collectionId: UUID`, `environmentId: UUID`, `scheduleCron: string`, `p95LatencySlaMs: Decimal128`, `consecutiveFailuresThreshold: int`, `currentFailureStreak: int`, `uptime30dPct: Decimal128`, `tlsCertDaysRemaining: int?`, `healthStatus: enum(HEALTHY, DEGRADED_LATENCY, FAILING_OUTAGE, PAUSED)`, `triggerCanaryRollback: boolean`, `activeWorkItemId: UUID?`, `lastCheckedAt: datetime?`, `version: int` | `collectionId -> DevApiCollection.id`; `environmentId -> DevApiEnvironment.id`; `activeWorkItemId -> Platform WorkItem.id`. | Reaching `consecutiveFailuresThreshold` transitions `healthStatus` to `FAILING_OUTAGE`, creates a high-priority SRE Home `WorkItem`, and emits `dev.api.monitor.breached.v1` (triggering `#102` Canary rollback when `triggerCanaryRollback: true`). |

---

## 5. Core End-to-End User Journeys (5 Journeys)

1. **Journey 1 — Design-First Spec Authoring, Instant Mock Server & Parallel Frontend Build:**
   - A Backend Architect creates `Orders API v2.1` (`OPENAPI_3_1`) in `api-specs`, verifies `0` Spectral lint errors (`API-002`) and `98.5%` AI-agent schema readiness (`API-006`) on `spec-test-detail`, and clicks `"Spin Up Mock Server"`.
   - `mock-servers` provisions `/mocks/orders-v2` (`DevMockServer`) with optional `15%` `429` chaos testing (`API-020`), allowing the Frontend team to build and test retry states immediately before backend code merges.
2. **Journey 2 — Breaking Contract Diff Blocked & Routed via Architect Home `WorkItem`:**
   - A developer edits `Orders API v2.1` removing a required field `totalAmountDecimal` from `OrderResponse` and submits for `PUBLISHED` promotion.
   - The Semantic Diff Detector (`API-003`) flags `hasBreakingDiff = true`, blocks direct publication, creates a Rapider Home `WorkItem` for the Principal API Architect, and displays the side-by-side schema diff on `breaking-changes`.
3. **Journey 3 — Vault-Backed Request Chaining, Idempotency Replay & `#102` CI Contract Gate:**
   - In `request-workbench`, a QA Engineer chains `POST /auth/token` (binding `{{env.clientSecret}}` via `vaultSecretRef`) -> `POST /orders` (with `checkIdempotencyReplay: true` `API-017`) -> `GET /orders/{{createOrder.id}}` and syncs the collection to `#101` (`API-004`).
   - During `#102` `STAGING` deployment, `ci-cd` invokes `dev.api.executeTestRun`. `DevApiTestRun` verifies `201` creation, `200` idempotent replay with zero duplicate orders, and zero `CONTRACT_DRIFT` against `DevApiSpec`, unlocking `#102` `PRODUCTION` promotion.
4. **Journey 4 — Synthetic Monitor Outage Kanban Triage & `#102` Canary Auto-Rollback:**
   - Two minutes after a `#102` Canary shift, the `Checkout Critical Flow` `DevApiMonitor` fails twice (`502 Bad Gateway`), crossing `consecutiveFailuresThreshold: 2`.
   - `api-monitors` (`<rapider-kanban>` + table) moves the monitor card to `FAILING_OUTAGE`, emits `dev.api.monitor.breached.v1` (triggering `#102` Canary auto-rollback within seconds), and opens an SRE Home `WorkItem` with a credential-scrubbed failure trace (`API-028`).
5. **Journey 5 — Click-Through Navigation & State-Preserving Back Navigation:**
   - On `api-test-runs`, an engineer filters by `Status: "CONTRACT_DRIFT"` (`#activeFilterTagsBar` renders `Status: "CONTRACT_DRIFT" ✕`), clicks run `TRUN-4019` to inspect exact drifted fields on `#/spec-test-detail?id=...`, and clicks `"Back to Test Runs"`, restoring `Status: "CONTRACT_DRIFT"` intact.

---

## 6. Consolidated Feature Priorities & Work Packages (`P0`, `P1`, `P2`)

### `P0` Foundation Work Packages
- **`WP-P0-1` API Specs, Spectral Linting & Breaking-Change Guard (`API-001`, `API-002`, `API-003`):** Build `api-hub`, `api-specs`, `spec-test-detail`, `lint-governance`, and `breaking-changes` with OpenAPI/AsyncAPI validation and Home `WorkItem` breaking-diff approvals (`API Architect` / `Developer`).
- **`WP-P0-2` Multi-Protocol Workbench, Chaining & Zero-Secret Vault Environments (`API-007`, `API-008`, `API-009`):** Build `api-collections`, `request-workbench`, and `api-environments` supporting REST/GraphQL/gRPC/WS/SSE, JSONPath variable chaining, and strict `vaultSecretRef` binding (`Developer` / `QA`).
- **`WP-P0-3` Collection Runner, Contract Drift & Mock Servers (`API-013`, `API-014`, `API-015`, `API-019`):** Build `api-test-runs` and `mock-servers` with JSON Schema/OpenAPI contract drift detection and `#102`/`#101` CI gate integration (`QA` / `Frontend Dev`).
- **`WP-P0-4` Synthetic API Monitors & Canary Outage Escalation (`API-021`, `API-022`):** Build `api-monitors` (`<rapider-kanban>` + table) with `Decimal128` uptime/latency tracking, TLS expiry alerts, Home `WorkItem`s, and `#102` Canary breach events (`SRE`).

### `P1` Scale & Enterprise Governance Work Packages
- **`WP-P1-1` `#101` Git Sync, Suite Explorer, Snippets, Portal & Cloud Run URL Lint (`API-004`, `API-005`, `API-010`, `API-011`, `API-012`):** Build `developer-portal`, bi-directional `#101` Git branch sync, `.run.app`/ingress URL lint warnings, and multi-language snippet generation (`Developer`).
- **`WP-P1-2` OWASP API Fuzzing, Idempotency Helper, Chaos Mocks & BI Scorecard (`API-016`, `API-017`, `API-020`, `API-023`, `API-024`):** Non-destructive BOLA/auth negative suites, idempotency/version replay assertions, mock chaos injection + call inspector, and `#096` SLA metrics (`AppSec` / `QA`).

### `P2` Adjacent & Grounded AI Work Packages
- **`WP-P2-1` Agent Schema Validator, Smoke Load & Grounded AI Co-Author (`API-006`, `API-018`, `API-025`, `API-026`):** MCP/agent schema readiness scoring, verified-domain staging smoke load tests, and grounded AI test/spec generation (`Developer` / `QA`).
- **`WP-P2-2` AI Contract Failure Explainer & Redacted Bug Snapshots (`API-027`, `API-028`):** Header-scrubbed `4xx/5xx` RCA over `projectChannelMessage` and 1-click redacted bug snapshots linked to `APM` `ApmIssue`s (`Developer` / `Support`).

---

## 7. Roles, Permissions & Field-Level Governance

| Role | Permitted Actions | Restricted / Field-Level Boundaries |
| :--- | :--- | :--- |
| **`Portal Consumer`** | Browse `PUBLISHED` specs in `developer-portal`, copy client snippets, invoke permitted `DevMockServer` endpoints. | Cannot view `DRAFT` internal specs, edit collections, or execute server-side runs against `PRODUCTION` environments. |
| **`Developer / QA Engineer`** | Create/edit `DevApiSpec` (`DRAFT`), `DevApiCollection`, `DevApiRequestItem`, `DevMockServer`; run `DevApiTestRun`s in `LOCAL/DEV/STAGING`. | Cannot self-approve breaking changes on `PUBLISHED` specs; cannot read raw secret values behind `vaultSecretRef`. |
| **`API Platform Architect`** | Configure workspace `lint-governance` Spectral rules, approve/reject breaking `DevApiSpec` diffs via Home `WorkItem`s, publish specs to `developer-portal`. | All breaking-change overrides require documented consumer migration notes and immutable audit logging. |
| **`AppSec / Security Tester`** | Run `OWASP_SECURITY` `DevApiTestRun` fuzzing suites against authorized `DEV/STAGING` targets, review BOLA/auth findings. | `OWASP_SECURITY` and `SMOKE_LOAD` runs against unverified external domains or `PRODUCTION` are deterministically blocked. |
| **`SRE / Monitor Admin`** | Manage `PRODUCTION` `DevApiEnvironment` vault bindings, configure `DevApiMonitor` cron schedules and `triggerCanaryRollback` links to `#102`. | Every `PRODUCTION` environment edit emits a security audit event. |

---

## 8. Technical APIs, Guarded Commands, Events & `requiredWorkflows`

### Guarded Commands
1. `dev.api.lintAndPublishSpec({ specId, targetStatus, approveBreakingOverride, reviewNotes, expectedVersion, idempotencyKey, correlationId })` — Runs Spectral linter + semantic diff against prior `PUBLISHED` version; blocks breaking diffs unless approved by `API Platform Architect` and resolves Home `WorkItem`.
2. `dev.api.executeTestRun({ collectionId, environmentId, runMode, cicdPipelineRunId, idempotencyKey, correlationId })` — Validates SSRF egress guardrails, resolves `vaultSecretRef` in isolated worker memory, runs chained requests + contract/idempotency assertions, scrubs auth headers, and writes `DevApiTestRun`.
3. `dev.api.manageMockServer({ mockServerId, specId, chaosConfig, status, expectedVersion, idempotencyKey, correlationId })` — Updates spec-driven mock routing and chaos rules atomically.
4. `dev.api.evaluateSyntheticMonitor({ monitorId, idempotencyKey, correlationId })` — Executes synthetic probe, updates `Decimal128` rolling uptime & TLS countdown, escalates Home `WorkItem`s, and emits Canary breach signals.

### Domain Events Published & Consumed (Kafka)
- **Published:** `dev.api.spec.published.v1`, `dev.api.spec.breaking_change_detected.v1`, `dev.api.test_run.completed.v1` (consumed by `#101` & `#102`), `dev.api.monitor.breached.v1` (consumed by `#102` Canary rollback), `dev.api.monitor.recovered.v1`.
- **Consumed:** `dev.scm.push.accepted.v1` (from `#101` to sync Git-backed specs/collections), `dev.cicd.deployment.succeeded.v1` (from `#102` to trigger post-deploy contract smoke runs).

### `requiredWorkflows`
- `apiSyntheticMonitorCronWorkflow` — Multi-step scheduled endpoint health & TLS certificate check with Home `WorkItem` and `#102` Canary rollback emission.
- `apiBreakingSpecApprovalWorkflow` — Routes breaking OpenAPI/AsyncAPI contract diffs to `API Platform Architect` Home `WorkItem`s.
- `apiGitCollectionSyncWorkflow` — Bi-directional declarative spec/collection synchronization with `#101` repositories (verifying zero secrets before commit).

### Grounded Rapider AI Governance Rules
- AI test/spec generators (`API-025`–`API-027`) strictly strip `Authorization`, `Cookie`, and `vaultSecretRef` values before prompt construction, ground assertions strictly in `DevApiSpec` schemas, and **NEVER** execute mutation requests against `PRODUCTION` `DevApiEnvironment`s or approve breaking contract changes autonomously.

---

## 9. Security, Privacy, Compliance & Non-Functional Requirements

- **SSRF & Sandbox Boundary Protection (OWASP / SOC 2):** Server-side request execution (`executeTestRun`, `evaluateSyntheticMonitor`) strictly blocks loopback (`127.0.0.0/8`, `::1`), cloud instance metadata (`169.254.169.254`), and undocumented internal host services unless explicitly allowlisted by platform infrastructure policy; `SMOKE_LOAD` and `OWASP_SECURITY` modes require verified workspace-owned `STAGING/DEV` domains.
- **Zero-Secret Persistence & Header Redaction:** Plaintext secrets in `DevApiEnvironment` (`isSecret: true`), `DevApiRequestItem` headers, Git exports, and `DevApiTestRun` logs are deterministically rejected or scrubbed (`***REDACTED***`).
- **Cloud Run Endpoint Hygiene:** Environment URL linters verify that public Google Cloud Run API deployments use direct `.run.app` URLs with proper ingress configuration to prevent SSL handshake and internal-ingress `403` failures.
- **Precision & Host Tenancy:** `Decimal128` used for `uptime30dPct`, `p95LatencyMs`, `agentReadinessScorePct`, and `chaosFailureRatePct`; zero `projectId` fields on models.
- **Accessibility & Responsive UX:** `<rapider-kanban>` on `api-monitors` syncs live with its table view; WCAG 2.2 AA accessible keyboard tabs in `request-workbench`, `#ffffff !important` white text on primary/danger buttons across `390px`, `768px`, and `1440px`.

---

## 10. Deterministic Acceptance Criteria (15 Testable Criteria)

1. **AC-01 (Sidebar Minimum-3 Rule):** Visible sidebar sections (`Design & Collections`: 4 items, `Testing & Mocking`: 3 items, `Governance & Monitoring`: 3 items) each contain `>= 3` `displayOnMenu: true` pages; `request-workbench`, `spec-test-detail`, and `api-entity-drawer` set `displayOnMenu: false`.
2. **AC-02 (Rapider Kanban & Multi-View Sync):** `api-monitors` renders `<rapider-kanban>` synchronized with its table view; pausing or resolving a monitor optimistically updates both views without reload.
3. **AC-03 (SWR Clean Queries & Defensive Soft-Delete):** All 10 sidebar routes load via `findSWR`/`countSWR` with zero `isDeleted` client where-clauses and apply in-memory `item.isDeleted !== true` filtering.
4. **AC-04 (Table Actions & Real Click-Through):** Zero `"View"` buttons exist in `Actions` columns; clicking a spec name on `api-specs` navigates to `#/spec-test-detail?id=...` and clicking a collection on `api-collections` navigates to `#/request-workbench?collectionId=...` without `<base href>` 404 traps; `Edit` uses icon+text and `Delete` uses an icon-only button with `#rapiderConfirmOkBtn` modal confirmation.
5. **AC-05 (Active Filter Tags & Clear All):** Filtering `api-specs`, `api-test-runs`, or `api-monitors` displays `#activeFilterTagsBar` with HTML-escaped dismissible chips and `[Clear all]`.
6. **AC-06 (Drawer Lifecycle & `finally` Reset):** Creating/editing an environment, mock server, or monitor in `api-entity-drawer` restores button state inside `finally`, clears SWR caches, updates parent lists/kanban optimistically, and closes the drawer via `closePageDrawer()`.
7. **AC-07 (Zero-Secret Environment & Header Guard):** Saving a `DevApiEnvironment` variable with `isSecret: true` and a non-null `plainValue` (or a `DevApiRequestItem` with a hardcoded `Bearer ...` token) fails validation (`422 Use Vault Secret Reference`), and captured `DevApiTestRun` logs redact `Authorization` and `Cookie` headers.
8. **AC-08 (SSRF Metadata & Unverified Load-Test Block):** Executing `dev.api.executeTestRun` targeting `http://169.254.169.254/...` or `localhost` internal ports—or running `SMOKE_LOAD` / `OWASP_SECURITY` against an unverified third-party domain—is deterministically rejected (`403 Egress Policy Blocked`).
9. **AC-09 (Breaking Spec Promotion Gate & Home `WorkItem`):** Calling `dev.api.lintAndPublishSpec({ targetStatus: 'PUBLISHED' })` when `lintErrorsCount > 0` fails (`422`), and when `hasBreakingDiff === true` without `API Platform Architect` override approval routes to `IN_REVIEW` and creates a Rapider Home `WorkItem`.
10. **AC-10 (Contract Drift Detection):** When a staging endpoint returns a response violating a required field or type in the linked `DevApiSpec`, `DevApiTestRun.status` records `CONTRACT_DRIFT` with exact field paths in `contractDriftItemsJson`.
11. **AC-11 (Idempotency Replay Verification):** Enabling `checkIdempotencyReplay: true` on a `POST` `DevApiRequestItem` replays the request with the identical `Idempotency-Key` and fails the test run if the target service creates a duplicate record or returns `500`.
12. **AC-12 (Monitor Breach -> `#102` Canary Auto-Rollback Event):** When a `DevApiMonitor` (`triggerCanaryRollback: true`) reaches `consecutiveFailuresThreshold`, it transitions to `FAILING_OUTAGE`, opens an SRE Home `WorkItem`, and emits `dev.api.monitor.breached.v1`.
13. **AC-13 (`Decimal128` SLA & Financial Schema Fidelity):** Rolling `uptime30dPct`, `p95LatencyMs`, and `Decimal128` monetary field contract assertions preserve exact precision.
14. **AC-14 (Back Navigation Filter Preservation):** Navigating from `api-test-runs` (filtered by `Status: "CONTRACT_DRIFT"`) to `spec-test-detail` and clicking `#btnGoBack` restores `api-test-runs` with `Status: "CONTRACT_DRIFT"` intact.
15. **AC-15 (Theme & Contrast Compliance):** All routes pass light/dark `validate_theme` checks with `#ffffff !important` white text on primary/danger buttons and zero `window.alert`/`confirm`/`prompt` dialogs.
