# 1. Project proposal

| Field | Value |
|---|---|
| Title (EN) | Development of an AI-Based System for Automated Generation of Software Test Cases from Requirements Documents Using a Local Language Model |
| Type | Diploma project (group, 3 students), educational programme Software Engineering |
| Team | Nuraly Abat (Role A), Sultan Muratbek (Role B), Kaisar Yessenov (Role C) |
| Supervisor | Almas Ospanov, Senior Lecturer, School of Software Engineering |
| Repository | https://github.com/yssnov/ai-testcase-generator · Notion task board: `<board URL>` |

## 1.1 Problem statement

Test cases are usually written by hand from requirements documents. This is slow, depends on the tester's experience, and requirements are often left without tests, which is discovered late, when fixing is expensive [ASSUMPTION — to be checked in interviews, see 02]. General-purpose cloud LLMs can draft test cases from requirements: recent studies report that most generated cases are judged valid or helpful, but correctness still requires human review [VERIFIED — L7, L9, L10 in the literature review]. Many organisations (banks, public sector, companies with confidential projects) are not allowed to send requirement documents to external AI services [ASSUMPTION — to be checked in interviews]. A local, self-hosted open-weight model avoids this barrier, but its quality, structure, speed and cost for this task are not well measured, especially for Russian- and Kazakh-language requirements [ASSUMPTION — partially supported by the literature gap noted in 03].

## 1.2 Target users

- **QA engineers / test analysts** — primary users; prepare test suites.
- **Business analysts** — check requirement testability.
- **Team leads** — need traceability and coverage.
- Context: IT teams in Kazakhstan/CIS organisations with restrictions on external AI services.

## 1.3 Aim

To develop and evaluate a web-based system that automatically generates traceable software test cases from requirements documents using a locally hosted language model, with mandatory human review.

## 1.4 Objectives

1. Analyse research and existing tools for requirements-based and LLM-based test generation (03, 04).
2. Collect evidence from 3–5 potential users on how test cases are written today and what blocks AI use (02).
3. Specify functional and non-functional requirements with acceptance criteria (06).
4. Design the architecture, data model and user interface (07, 08).
5. Implement the MVP: upload → extraction → generation → review → export, with traceability.
6. Build a requirements dataset with gold test cases and benchmark 3–4 local models and prompting strategies (09).
7. Verify the system with unit, integration, end-to-end, load and security tests, and a user study (09).

## 1.5 Expected outcomes (measurable)

| Outcome | Measure |
|---|---|
| Working system deployed in production mode | Full flow demonstrated on a public requirements document |
| Generation quality | Requirement coverage, schema-valid rate, duplicate rate, hallucination rate, expert acceptance rate vs baselines (09) |
| Performance | Load test at the target of ~1,000 users/day; p95 latency targets (06, NFR) |
| Usability and effort | SUS score; time to produce an accepted test suite vs manual baseline |
| Reproducibility | Dataset, prompts, scripts and raw results in the repository |

## 1.6 Scope

| In scope (Must, by end of January 2027) | Should (by March) | Won't (this project) |
|---|---|---|
| Auth with roles; projects; requirement quality gate (ISO/IEC/IEEE 29148 checks) before generation | — | Executable test script generation |
| Upload PDF/DOCX/MD; requirement extraction with IDs | RAG context from project documents | Test execution |
| Generation with a local LLM, JSON-schema validated | Verifier step (dedupe, grounding) | Billing, SSO, mobile apps |
| Review workspace: accept / edit / reject / regenerate | EN/RU/KK user interface | Multi-tenant SaaS |
| Traceability matrix and coverage | Evaluation dashboard | |
| Export CSV, XLSX, Gherkin, JSON | Jira/TestRail/Xray CSV formats (Could) | |

## 1.7 Engineering complexity (why this is a diploma project, not a CRUD app)

- **Requirements engineering and test design:** requirement segmentation, ISO/IEC/IEEE 29148 quality checks, ISO/IEC/IEEE 29119-4 test techniques (equivalence partitioning, boundary values, decision tables, state transitions).
- **LLM engineering:** schema-constrained generation, retrieval-augmented context, hallucination control, prompt-injection defence for uploaded documents, local model serving and capacity planning.
- **Full-stack system:** web UI, REST API with streaming progress, PostgreSQL with vector search, job queue, CI/CD, containerised deployment, monitoring.
- **Empirical evaluation:** dataset with gold cases, multiple models and baselines, inter-rater agreement, statistical tests, load and security testing.

## 1.8 Constraints and assumptions

- Budget for infrastructure: up to USD 50 for the whole project.
- Inference requires a GPU (≥12 GB VRAM) owned by the team or provided by the university [ASSUMPTION — confirm by 31 October].
- Only public or synthetic requirements documents are used; no personal or confidential data.
