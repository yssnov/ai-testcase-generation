# 6. Requirements Specification

Every Must requirement has an acceptance criterion that a test, a measurement or a demonstration can check. Priorities: M – Must (MVP, January 2027), S – Should (March 2027), C – Could. The Source column shows where a requirement comes from (H – hypothesis from Section 2, L – literature, E – existing systems); hypotheses will be updated after the interviews.

## 6.1 Actors

*Table 6.1 – Actors*

| Actor | Description |
|---|---|
| QA engineer (reviewer) | Uploads documents, generates, reviews and exports test cases |
| Business analyst | Uploads documents, reviews requirement quality flags |
| Administrator | Manages users and model configuration, views job metrics |
| Local LLM server (external system) | Generates JSON through an OpenAI-compatible API inside the organisation network |
| Test management tool (external system) | Receives exported files (CSV, XLSX, Gherkin, JSON) |

## 6.2 Functional Requirements

*Table 6.2 – Functional requirements*

| ID | Requirement | Pri | Acceptance criteria | Source | Owner |
|---|---|---|---|---|---|
| FR-01 | Users register and log in; roles reviewer and admin | M | Valid credentials → session cookie set; admin-only endpoints return 403 for reviewers (automated API tests) | Security baseline | Sultan Muratbek |
| FR-02 | Upload of a requirements document (PDF, DOCX, Markdown, TXT, ≤ 10 MB) into a project | M | The 4 formats are accepted; other types and files > 10 MB are rejected with a clear message (tests with sample files) | H6, L6 | Sultan Muratbek |
| FR-03 | Extraction of individual requirements with stable IDs; the user can edit, merge or split them | M | ≥ 90 % of requirements extracted as separate items on 5 reference documents (vs a manual list); IDs unchanged after re-opening | L2, L6 | Sultan Muratbek |
| FR-04 | Quality gate: flags ambiguous or incomplete requirements (vague words, missing values or units, missing actor or condition) before generation, based on ISO/IEC/IEEE 29148 | M | Flags shown per requirement; flag precision ≥ 70 % on a labelled sample of 50 requirements | H4, L6, L12, S1 | Nuraly Abat (+ Sultan Muratbek) |
| FR-05 | User selects requirements and test techniques and starts generation; progress shown live; job can be cancelled | M | Output validates against the JSON schema; progress events visible; cancel works (e2e test with a fake LLM; demo with a real model) | H1, L7, L9 | Sultan Muratbek, Nuraly Abat |
| FR-06 | Every generated case references ≥ 1 existing requirement ID; cases with unknown IDs are rejected and regenerated | M | 0 stored cases with non-existent requirement IDs (database constraint + unit tests) | L14, L18 | Nuraly Abat |
| FR-07 | Verifier flags likely duplicates and cases not grounded in the requirement text | S | Duplicate-flag precision ≥ 80 % on a labelled sample; flags visible in review | L9, L22 | Nuraly Abat |
| FR-08 | Reviewer accepts, edits, rejects or regenerates each case; bulk actions; every decision is logged | M | All four actions pass e2e tests; an audit-log row is created for each status change (trigger test) | H5, L7 | Kaisar Yessenov (UI), Sultan Muratbek (audit) |
| FR-09 | Traceability matrix (requirement × cases) and coverage % per document | M | Coverage % equals the share of requirements with ≥ 1 non-rejected case (SQL view test on fixture data) | H2, L14 | Kaisar Yessenov |
| FR-10 | Export of accepted cases to CSV, XLSX, Gherkin (.feature) and JSON | M | Each file opens in Excel/LibreOffice or a Gherkin parser without errors; round-trip test keeps all fields | H6, L10 | Sultan Muratbek |
| FR-11 | Export in Jira/Xray, TestRail and Qase import formats | C | Import into a trial instance succeeds (screenshot evidence) | H6, E1–E3 | Sultan Muratbek |
| FR-12 | Generation uses context retrieved from the same project (glossary, related requirements) | S | Ablation in Section 9 shows the effect of RAG on coverage and correctness | L7, L15, L25 | Nuraly Abat |
| FR-13 | Administrator selects the active model and sees job history (model, prompt version, tokens, latency, status) | M | Switching the model changes it in new jobs; job history lists the required fields | Section 9 | Sultan Muratbek |
| FR-14 | Evaluation harness runs a dataset with gold cases against a model/prompt configuration and writes a metrics report | M | One command produces a CSV/JSON report with the metrics of Section 9.5 | L6, Section 9 | Nuraly Abat |

## 6.3 Non-Functional Requirements

*Table 6.3 – Non-functional requirements*

| ID | Requirement | Pri | Acceptance criteria (conditions in Section 9) | Owner |
|---|---|---|---|---|
| NFR-PERF-01 | Responsive non-AI API | M | p95 < 300 ms at 50 concurrent virtual users (k6) | Sultan Muratbek |
| NFR-PERF-02 | Capacity for ~1 000 users/day | M | 2 000 generation jobs/day, peak 10 parallel jobs; queue wait p95 < 30 s; error rate < 1 % (load test) | Sultan Muratbek |
| NFR-PERF-03 | Generation latency | S | Time to first token < 5 s; batch of 10 requirements < 90 s (p95, reference GPU) | Nuraly Abat |
| NFR-REL-01 | No lost jobs | M | Killing the worker mid-job leads to retry and completion; 0 lost jobs in 20 trials | Sultan Muratbek |
| NFR-REL-02 | Atomic results | M | A job's cases, links and status are committed in one transaction (test with forced failure) | Sultan Muratbek |
| NFR-REL-03 | Availability and recovery | S | ≥ 99 % uptime during the 30-day evaluation month; database restore < 30 min (drill) | Sultan Muratbek |
| NFR-SEC-01 | Authentication hardening | M | Argon2id hashes; HttpOnly + Secure + SameSite cookies; login rate limit | Sultan Muratbek |
| NFR-SEC-02 | Authorisation | M | A user cannot read or change another user's projects (IDOR tests on every endpoint) | Sultan Muratbek |
| NFR-SEC-03 | Upload safety | M | Type allow-list, size limit, parsing in the worker, no macro execution (negative tests) | Sultan Muratbek |
| NFR-SEC-04 | Prompt-injection resilience | M | On 20 red-team documents with hidden instructions, output stays schema-valid and no instruction is executed | Nuraly Abat |
| NFR-SEC-05 | Audit trail | M | Review decisions logged with user and time (trigger test) | Sultan Muratbek |
| NFR-SEC-06 | Secrets management | M | No secrets in Git (secret scan in CI passes); configuration from environment variables | Sultan Muratbek |
| NFR-PRIV-01 | Data stays local (100 % on-premise) | M | No outbound calls to external AI APIs in production (egress check during the load test) | Sultan Muratbek |
| NFR-AIQ-01 | Structured output reliability | M | ≥ 95 % of generations schema-valid within ≤ 2 retries on the evaluation set | Nuraly Abat |
| NFR-AIQ-02 | Requirement coverage | S | ≥ 80 % of requirements receive ≥ 1 accepted case on the evaluation set | Nuraly Abat |
| NFR-AIQ-03 | Hallucination control | S | ≤ 10 % of cases contain features, values or limits not present in the source requirement (labelled sample ≥ 100 cases, 2 raters) | Nuraly Abat |
| NFR-USAB-01 | Usability | S | SUS ≥ 68 with ≥ 5 participants | Kaisar Yessenov |
| NFR-USAB-02 | Accessibility | S | WCAG 2.2 AA basics; Lighthouse accessibility ≥ 90 on core screens | Kaisar Yessenov |
| NFR-LANG-01 | Requirement languages | M | EN and RU documents processed and evaluated; KK evaluated on a small set and reported | Nuraly Abat |
| NFR-LANG-02 | UI languages | S | UI in EN, RU, KK; no hard-coded strings (lint check) | Kaisar Yessenov |
| NFR-MAINT-01 | Test quality gates | M | All tests pass before merge; ≥ 95 % line coverage of domain/service code (CI report) | All |
| NFR-MAINT-02 | Replaceable components | M | API documented in OpenAPI; LLM runtime and model changed by configuration only (contract tests on 2 runtimes) | Nuraly Abat |
| NFR-OPS-01 | Operability | M | Deployment with one command; health endpoints; monitoring dashboard; nightly encrypted backups | Sultan Muratbek |

## 6.4 Constraints

*Table 6.4 – Constraints*

| ID | Constraint |
|---|---|
| C-01 | Production uses only locally hosted open-weight models; no external AI APIs. A cloud model may be used only as an evaluation reference on public documents. |
| C-02 | Infrastructure budget ≤ USD 50 for the whole project. |
| C-03 | Only public, synthetic or explicitly permitted documents; no personal data. |
| C-04 | Pre-defense 1 on 24 October 2026; MVP by the end of January 2027. |
| C-05 | Inference requires a GPU with ≥ 12 GB VRAM (team-owned or provided by the university). |
