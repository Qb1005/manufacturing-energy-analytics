# Manufacturing Energy Analytics — Issue Roadmap

Planning only: these issue bodies have not yet been published to GitHub.

Phases 1–7 deliver the dashboard MVP. Phases 8–11 complete infrastructure, ingestion, security, and portfolio capabilities. No implementation is marked complete.

# Phase 1 — Business scope and source contract

## Objective
Complete business scope and source contract for the manufacturing energy analytics portfolio.

## Sub-issues
- [ ] 1.1 — Define the manufacturing energy use case
- [ ] 1.2 — Record source provenance and profile the dataset
- [ ] 1.3 — Approve architecture and delivery contract

## Completion gate
All child issues have verified acceptance criteria and attached evidence. Parent completion does not substitute for child verification.

## Dependency
Start after project scope review.


---

# 1.1 — Define the manufacturing energy use case

## Objective
Agree on the decisions the dashboard will support.

## Acceptance criteria
- [ ] Define audience: plant energy analyst and operations manager.
- [ ] Define total kWh, daily/monthly trends, load-type share, and highest-consumption intervals.
- [ ] Exclude OEE, downtime, yield, energy per manufactured unit, and actual cost savings because source inputs are absent.

## Required evidence
docs/business-case.md and reviewed KPI dictionary.

## Dependencies
None; first implementation issue.

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 1.2 — Record source provenance and profile the dataset

## Objective
Establish a reproducible real-data baseline.

## Acceptance criteria
- [ ] Download the original UCI dataset and record URL, attribution, retrieval date, and SHA-256.
- [ ] Profile actual rows, columns, date range, cadence, duplicate timestamps, missing values, and categories.
- [ ] Resolve timestamp parsing and interval-boundary semantics; document timezone assumptions and ambiguous CO2 units.

## Required evidence
Source manifest, profiling output, data dictionary, and cited limitations.

## Dependencies
1.1

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 1.3 — Approve architecture and delivery contract

## Objective
Freeze the MVP and the boundaries between tools.

## Acceptance criteria
- [ ] Document source → landing → RAW → dbt marts → Streamlit flow.
- [ ] Define owners: Schemachange for ingestion/control objects, dbt for models, app deployment for Streamlit, Terraform for selected infrastructure.
- [ ] Confirm Snowflake account availability, explicit warehouse runtime support, cost controls, dashboard acceptance criteria, and issue dependencies.

## Required evidence
Architecture diagram, ownership matrix, and scope decision.

## Dependencies
1.2

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# Phase 2 — Repository and GitHub CI foundation

## Objective
Complete repository and github ci foundation for the manufacturing energy analytics portfolio.

## Sub-issues
- [ ] 2.1 — Bootstrap a reproducible repository
- [ ] 2.2 — Implement useful offline checks
- [ ] 2.3 — Protect main and establish evidence tracking

## Completion gate
All child issues have verified acceptance criteria and attached evidence. Parent completion does not substitute for child verification.

## Dependency
Phase 1; later extension work must preserve the dashboard MVP.


---

# 2.1 — Bootstrap a reproducible repository

## Objective
Make a fresh checkout usable on macOS.

## Acceptance criteria
- [ ] Create README, Python environment instructions, dependency versions, .gitignore, and configuration examples without secrets.
- [ ] Create src, tests, migrations, dbt, app, docs, and evidence directories.
- [ ] Add source attribution and distinguish data license from project code license.

## Required evidence
Setup PR and clean-environment verification.

## Dependencies
Phase 1

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 2.2 — Implement useful offline checks

## Objective
Detect code and data-contract defects before deployment.

## Acceptance criteria
- [ ] Create unit tests for timestamp parsing, file identity, duplicate handling, and invalid rows.
- [ ] Run Ruff, pytest, and SQLFluff over maintained SQL directories in PR CI.
- [ ] Use correct templating for migration SQL; introduce dbt templating when dbt models exist.

## Required evidence
Passing CI plus a deliberate failing test and corrective PR.

## Dependencies
2.1

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 2.3 — Protect main and establish evidence tracking

## Objective
Require reviewed changes and record learning.

## Acceptance criteria
- [ ] Configure required checks and PR-only changes under the account capabilities.
- [ ] Demonstrate failed checks blocking merge.
- [ ] Link issues, PRs, run attempts, commit SHA, results, and limitations in the Project.

## Required evidence
Ruleset evidence and passing/failing PR links.

## Dependencies
2.2

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# Phase 3 — Snowflake environments and access

## Objective
Complete snowflake environments and access for the manufacturing energy analytics portfolio.

## Sub-issues
- [ ] 3.1 — Bootstrap isolated environments
- [ ] 3.2 — Configure roles and service access
- [ ] 3.3 — Verify connections and restrictions

## Completion gate
All child issues have verified acceptance criteria and attached evidence. Parent completion does not substitute for child verification.

## Dependency
Phase 2; later extension work must preserve the dashboard MVP.


---

# 3.1 — Bootstrap isolated environments

## Objective
Keep lab development separate from the promoted release.

## Acceptance criteria
- [ ] Create MFG_DEV, MFG_TEST, MFG_PROD with RAW, STAGING, MARTS, OPS, and BI schemas.
- [ ] Configure a small warehouse, auto-suspend, and supported usage monitoring.
- [ ] Record bootstrap objects and future Terraform ownership; do not reuse or replace old demo objects.

## Required evidence
Environment inventory and bootstrap SQL.

## Dependencies
Phase 2

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 3.2 — Configure roles and service access

## Objective
Give each task the privileges it needs.

## Acceptance criteria
- [ ] Define deployment, ingestion, transformation, and dashboard access boundaries.
- [ ] Configure GitHub environments and credentials without committing secrets.
- [ ] Document shared identities versus role isolation and required Streamlit owner privileges.

## Required evidence
Role matrix and environment-variable names.

## Dependencies
3.1

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 3.3 — Verify connections and restrictions

## Objective
Prove configuration selects the intended target.

## Acceptance criteria
- [ ] Verify role, database, schema, and warehouse in all environments.
- [ ] Test a denied cross-environment operation using the intended role context.
- [ ] Confirm supported authentication for the available account and tools.

## Required evidence
Positive/negative access results and workflow logs.

## Dependencies
3.2

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# Phase 4 — Schemachange and reliable source loading

## Objective
Complete schemachange and reliable source loading for the manufacturing energy analytics portfolio.

## Sub-issues
- [ ] 4.1 — Version ingestion and audit objects
- [ ] 4.2 — Implement validated batch ingestion
- [ ] 4.3 — Verify replay and duplicate handling

## Completion gate
All child issues have verified acceptance criteria and attached evidence. Parent completion does not substitute for child verification.

## Dependency
Phase 3; later extension work must preserve the dashboard MVP.


---

# 4.1 — Version ingestion and audit objects

## Objective
Make the raw-layer setup repeatable.

## Acceptance criteria
- [ ] Create migrations for raw records, load manifest, rejected rows, and deployment history.
- [ ] Define raw record identity as file checksum plus source row number; establish canonical interval key after profiling.
- [ ] Run a V migration and verify history; keep deployed V files unchanged.

## Required evidence
Migration PR, object definitions, and history export.

## Dependencies
Phase 3

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 4.2 — Implement validated batch ingestion

## Objective
Load source records with traceability.

## Acceptance criteria
- [ ] Preserve original file and raw values; attach filename, checksum, row number, and ingestion timestamp.
- [ ] Validate required columns and parse rules; quarantine invalid records with reasons.
- [ ] Record batch status and counts; reconcile source = accepted + rejected under the defined duplicate policy.

## Required evidence
Successful DEV load and reconciliation report.

## Dependencies
4.1

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 4.3 — Verify replay and duplicate handling

## Objective
Make retrying a file safe.

## Acceptance criteria
- [ ] Load the same file twice and prove no duplicate canonical records.
- [ ] Test malformed input and an interrupted/failed batch then recover.
- [ ] Split historical data into chronological files for a clearly labeled batch-arrival simulation; never describe it as a live feed.

## Required evidence
Duplicate/failure test output and ingestion runbook.

## Dependencies
4.2

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# Phase 5 — dbt analytical models and quality

## Objective
Complete dbt analytical models and quality for the manufacturing energy analytics portfolio.

## Sub-issues
- [ ] 5.1 — Initialize dbt and staging models
- [ ] 5.2 — Build energy dimensions and facts
- [ ] 5.3 — Add meaningful tests and documentation

## Completion gate
All child issues have verified acceptance criteria and attached evidence. Parent completion does not substitute for child verification.

## Dependency
Phase 4; later extension work must preserve the dashboard MVP.


---

# 5.1 — Initialize dbt and staging models

## Objective
Convert raw values into typed, documented fields.

## Acceptance criteria
- [ ] Configure dbt Core with compatible Snowflake adapter and external credentials.
- [ ] Declare sources and create staging models with explicit timestamp and numeric conversions.
- [ ] Retain lineage back to source file and row; reject or flag ambiguous mappings.

## Required evidence
dbt compile/build output and staging reconciliation.

## Dependencies
Phase 4

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 5.2 — Build energy dimensions and facts

## Objective
Provide consistent analytical grain for the dashboard.

## Acceptance criteria
- [ ] Create dim_date, dim_time, dim_load_type, and fct_energy_interval.
- [ ] Create daily/monthly aggregates with documented date boundaries and complete-period handling.
- [ ] Use SUM for interval kWh; label maximum interval kWh separately from instantaneous peak power; do not sum power-factor percentages.

## Required evidence
Model SQL, grain/key documentation, and reconciled totals.

## Dependencies
5.1

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 5.3 — Add meaningful tests and documentation

## Objective
Detect errors that would mislead dashboard readers.

## Acceptance criteria
- [ ] Test keys, relationships, accepted load types, nonnegative consumption, timestamp gaps, and source-to-mart totals.
- [ ] Create a controlled bad-data fixture and verify a failing test.
- [ ] Generate dbt documentation and record baseline row counts and KPI results.

## Required evidence
Passing/failing dbt results, lineage, and baseline metrics.

## Dependencies
5.2

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# Phase 6 — DEV → TEST → PROD release pipeline

## Objective
Complete dev → test → prod release pipeline for the manufacturing energy analytics portfolio.

## Sub-issues
- [ ] 6.1 — Implement dependent deployment stages
- [ ] 6.2 — Add PROD approval and deployment serialization
- [ ] 6.3 — Verify release consistency and recovery

## Completion gate
All child issues have verified acceptance criteria and attached evidence. Parent completion does not substitute for child verification.

## Dependency
Phase 5; later extension work must preserve the dashboard MVP.


---

# 6.1 — Implement dependent deployment stages

## Objective
Promote one selected code revision.

## Acceptance criteria
- [ ] Run migrations, controlled data load, dbt build, and validation in DEV then TEST.
- [ ] Use needs dependencies and environment-specific settings/history.
- [ ] Record commit SHA and source manifest version; block downstream work on failures.

## Required evidence
Release workflow PR and successful DEV/TEST run.

## Dependencies
Phase 5

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 6.2 — Add PROD approval and deployment serialization

## Objective
Require a deliberate production-lab release.

## Acceptance criteria
- [ ] Configure available PROD approval and document solo-project limitations.
- [ ] Use workflow concurrency shared by all relevant deployment entry points without canceling active migrations.
- [ ] Demonstrate TEST failure blocking PROD and a clean release waiting for approval.

## Required evidence
Failed run, approval record, and successful PROD run.

## Dependencies
6.1

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 6.3 — Verify release consistency and recovery

## Objective
Prove a release can be traced and safely repeated.

## Acceptance criteria
- [ ] Compare code revision, source manifest, migration history, dbt results, and KPI totals across environments.
- [ ] Rerun the same revision and verify V/R behavior and ingestion idempotency.
- [ ] Document TEST recovery and distinguish written procedures from tested recovery.

## Required evidence
History exports, rerun attempts, reconciliation, and recovery notes.

## Dependencies
6.2

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# Phase 7 — Streamlit in Snowflake dashboard

## Objective
Complete streamlit in snowflake dashboard for the manufacturing energy analytics portfolio.

## Sub-issues
- [ ] 7.1 — Design dashboard pages and metric contracts
- [ ] 7.2 — Build the browser dashboard on curated marts
- [ ] 7.3 — Validate and release the dashboard

## Completion gate
All child issues have verified acceptance criteria and attached evidence. Parent completion does not substitute for child verification.

## Dependency
Phase 6; later extension work must preserve the dashboard MVP.


---

# 7.1 — Design dashboard pages and metric contracts

## Objective
Make the final output understandable before styling.

## Acceptance criteria
- [ ] Specify Overview, Operating Patterns, and Data Quality pages.
- [ ] Define date and load-type filters, KPI formulas, units, and empty-state behavior.
- [ ] Use total kWh, daily/monthly trend, hour/day heatmap, load mix, and completeness; exclude CO2 until its unit is resolved.

## Required evidence
Wireframes and dashboard acceptance checklist.

## Dependencies
Phase 6

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 7.2 — Build the browser dashboard on curated marts

## Objective
Deliver an interactive application usable from macOS.

## Acceptance criteria
- [ ] Implement Streamlit views reading marts rather than reimplementing business logic.
- [ ] Add environment/source-period labels and distinguish ingestion time from historical measurement time.
- [ ] Check filter behavior, readable axes, and no-data handling; explicitly select the supported runtime.

## Required evidence
App code, Snowflake app link, screenshots, and filter checks.

## Dependencies
7.1

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 7.3 — Validate and release the dashboard

## Objective
Ensure visuals agree with the underlying data.

## Acceptance criteria
- [ ] Reconcile at least five displayed results with independent SQL queries across filters.
- [ ] Deploy the same reviewed app revision through environments and test viewer access.
- [ ] Record final app URL, release SHA, screenshots, metric limitations, and refresh/reload instructions.

## Required evidence
Dashboard acceptance results and release evidence.

## Dependencies
7.2

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# Phase 8 — Terraform infrastructure ownership

## Objective
Complete terraform infrastructure ownership for the manufacturing energy analytics portfolio.

## Sub-issues
- [ ] 8.1 — Plan and validate resource ownership
- [ ] 8.2 — Apply one controlled infrastructure change

## Completion gate
All child issues have verified acceptance criteria and attached evidence. Parent completion does not substitute for child verification.

## Dependency
Phase 7; later extension work must preserve the dashboard MVP.


---

# 8.1 — Plan and validate resource ownership

## Objective
Introduce IaC without recreating working resources.

## Acceptance criteria
- [ ] Inventory existing warehouses, schemas, roles, and grants; select a small supported Terraform scope.
- [ ] Choose import versus exclusion and document bootstrap dependencies.
- [ ] Configure provider versions and protected state; run format/validate and review a plan.

## Required evidence
Ownership/import plan and validation output.

## Dependencies
Phase 7

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 8.2 — Apply one controlled infrastructure change

## Objective
Demonstrate reviewed and reproducible infrastructure delivery.

## Acceptance criteria
- [ ] Import selected resources if required and review for unexpected replacement.
- [ ] Apply a small lab change with safe privileges and verify the result.
- [ ] Add PR validation/plan and an approved apply path with serialized state access.

## Required evidence
Reviewed plan, apply evidence, and drift/recovery notes.

## Dependencies
8.1

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# Phase 9 — AWS ingestion or labeled local simulation

## Objective
Complete aws ingestion or labeled local simulation for the manufacturing energy analytics portfolio.

## Sub-issues
- [ ] 9.1 — Define landing and event contracts
- [ ] 9.2 — Implement and test the chosen ingestion path

## Completion gate
All child issues have verified acceptance criteria and attached evidence. Parent completion does not substitute for child verification.

## Dependency
Phase 8; later extension work must preserve the dashboard MVP.


---

# 9.1 — Define landing and event contracts

## Objective
Extend the existing file loader without changing business metrics.

## Acceptance criteria
- [ ] Map file storage, event payload, batch identity, and duplicate-event behavior.
- [ ] Select real S3/Lambda only if account and budget allow; otherwise map local files and Python events explicitly.
- [ ] Retain the exact source snapshot and document historical replay as simulation.

## Required evidence
Ingestion contract and execution-mode decision.

## Dependencies
Phase 8

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 9.2 — Implement and test the chosen ingestion path

## Objective
Demonstrate observable file-to-Snowflake delivery.

## Acceptance criteria
- [ ] Implement file arrival → validation → existing loader with least-required access.
- [ ] Test duplicate events, malformed files, retry, and logs.
- [ ] Document setup, costs/limits, and teardown; do not claim AWS deployment for a local simulation.

## Required evidence
End-to-end batch evidence and failure/retry records.

## Dependencies
9.1

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# Phase 10 — Authentication and operational readiness

## Objective
Complete authentication and operational readiness for the manufacturing energy analytics portfolio.

## Sub-issues
- [ ] 10.1 — Harden supported service authentication
- [ ] 10.2 — Add operational traceability and recovery

## Completion gate
All child issues have verified acceptance criteria and attached evidence. Parent completion does not substitute for child verification.

## Dependency
Phase 9; later extension work must preserve the dashboard MVP.


---

# 10.1 — Harden supported service authentication

## Objective
Reduce credential exposure using compatible mechanisms.

## Acceptance criteria
- [ ] Inventory identities, credential storage, and tool support.
- [ ] Implement supported key-pair or federated authentication and narrower identities as feasible.
- [ ] Verify authorized access and a denied case; retire old credentials only after validation.

## Required evidence
Authentication matrix, redacted verification, and remaining limits.

## Dependencies
Phase 9

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 10.2 — Add operational traceability and recovery

## Objective
Make failed releases and loads diagnosable.

## Acceptance criteria
- [ ] Record release SHA, environment, batch ID, source checksum, and run link in summaries.
- [ ] Define actionable failure notifications and warehouse usage review.
- [ ] Rehearse one recovery scenario and document restore/forward-fix decisions and app impact.

## Required evidence
Operational dashboard/log examples and rehearsed runbook.

## Dependencies
10.1

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# Phase 11 — Portfolio acceptance and release

## Objective
Complete portfolio acceptance and release for the manufacturing energy analytics portfolio.

## Sub-issues
- [ ] 11.1 — Verify end-to-end reproducibility
- [ ] 11.2 — Publish the portfolio milestone

## Completion gate
All child issues have verified acceptance criteria and attached evidence. Parent completion does not substitute for child verification.

## Dependency
Phase 10; later extension work must preserve the dashboard MVP.


---

# 11.1 — Verify end-to-end reproducibility

## Objective
Confirm the repo matches the delivered system.

## Acceptance criteria
- [ ] Reproduce setup and a representative source load from documented prerequisites.
- [ ] Trace one dashboard metric back through mart, staging, raw, and source record.
- [ ] Separate implemented, simulated, and deferred capabilities; keep unresolved work visible.

## Required evidence
Reproducibility checklist and lineage walkthrough.

## Dependencies
Phase 10

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.


---

# 11.2 — Publish the portfolio milestone

## Objective
Prepare an interview-ready demonstration.

## Acceptance criteria
- [ ] Write README architecture, dataset attribution, business findings, limitations, and setup/teardown.
- [ ] Prepare a short demo showing PR gate, release approval, ingestion retry, and dashboard.
- [ ] Close only evidenced issues and create a release with app screenshots and artifact links.

## Required evidence
Release notes, demo script, and final acceptance report.

## Dependencies
11.1

### Evidence
- Pull request:
- Workflow run and attempt / commit SHA:
- Relevant output, SQL results, screenshot, or artifact:
- Expected versus observed result:

### Learning review
- What did I implement?
- Why is it needed?
- How did I verify it?
- What failed, and how did I fix it?
- What limitations remain?

### Definition of Done
- [ ] Acceptance criteria above are met.
- [ ] Evidence is attached and claims match observed results.
- [ ] Documentation and learning review are complete.
