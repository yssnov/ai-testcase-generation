# AI-Based Test Case Generator from Requirements (Local LLM)

> **Diploma project (group), Astana IT University, 2026–2027**
> **EN:** Development of an AI-Based System for Automated Generation of Software Test Cases from Requirements Documents Using a Local Language Model
> **KZ:** Жергілікті тілдік модельді қолдана отырып, талаптар құжаттары бойынша бағдарламалық қамтамасыздандыруды тестілеу сценарийлерін (test cases) автоматты генерациялауға арналған жасанды интеллект негізіндегі жүйені әзірлеу
> **RU:** Разработка системы на основе искусственного интеллекта для автоматической генерации тестовых сценариев (test cases) по документам требований с использованием локальной языковой модели

A web system that reads a software requirements document (SRS, user stories, PRD), extracts and checks the requirements, and generates **traceable, reviewable test cases** with a language model that runs on infrastructure the team controls. A QA engineer reviews, edits and accepts the cases and exports them to CSV/XLSX/Gherkin/JSON.

## Problem statement

Writing test cases from requirements by hand is slow, depends on the tester's experience, and often misses requirements. Cloud LLMs can draft test cases, but many organisations cannot send requirement documents to external AI services (confidentiality, data-localisation rules, cost, vendor lock-in). A locally hosted model removes that barrier, but its quality, reliability and cost must be measured before anyone relies on it.

## Target users

| User | Need |
|---|---|
| QA engineer / test analyst (primary) | Produce a reviewable test suite for a requirements document in minutes, not days |
| Business analyst | See which requirements are ambiguous or untestable before development |
| Team lead | See requirement → test traceability and coverage |

Evidence for these needs: see [docs/02-relevance-evidence](docs/02-relevance-evidence/README.md) (interviews, verified findings vs assumptions).

## Expected outcomes

1. A deployed web system covering the full flow: requirements document → extracted requirements → generated test cases → human review → export, with traceability.
2. A reproducible benchmark of 3–4 open-weight local models and prompting strategies on a requirements dataset with gold test cases.
3. Test, load and security reports, and a user study (SUS, time to prepare a test suite vs manual work).

## Team and responsibilities

| Member | Role | Owns |
|---|---|---|
| Nuraly Abat (`@wickylinn`) | **A — AI pipeline & evaluation** | LLM provider layer, prompts, generation/verification pipeline, traceability, dataset, model benchmark |
| Sultan Muratbek (`@mvxyqfxt`) | **B — Backend, data & DevOps** | Document parser, API, database, queue/worker, security, CI/CD, deployment, load tests |
| Kaisar Yessenov (`@yssnov`) | **C — Frontend, UX & QA** | UX research, prototype, web app, review/export flow, test strategy, e2e tests, user study |
| Almas Ospanov | **Supervisor** | Review of key deliverables and decisions ([feedback log](docs/11-supervisor-feedback-log.md)) |

## Scope

**In scope (MVP):** upload PDF/DOCX/Markdown; requirement extraction with stable IDs; requirement quality gate (ISO/IEC/IEEE 29148 checks) before generation; generation with a local LLM (schema-validated JSON); review workspace (accept/edit/reject); traceability matrix and coverage; export CSV/XLSX/Gherkin/JSON; model and prompt evaluation.
**Should (March 2027):** RAG over project documents, duplicate/grounding verifier, EN/RU/KK interface. **Could:** Jira/TestRail/Xray import formats, Kazakh-language evaluation, LoRA fine-tuning.
**Out of scope:** automated test script generation (Selenium/Playwright code), test execution, billing, SSO.
Details: [docs/01-project-proposal.md](docs/01-project-proposal.md).

## Current status

| Stage | Status |
|---|---|
| Proposal, scope | 🟢 ready for review |
| Relevance evidence (3–5 interviews) | 🟡 interviews in progress |
| Literature review (27 publications + 3 standards) | 🟢 ready for review |
| Existing systems comparison (5 systems × 9 criteria) | 🟡 "Not stated" cells to confirm |
| Technology comparison (6 decisions, 4 ADRs) | 🟢 ready for review |
| Requirements and acceptance criteria (14 FR, 23 NFR) | 🟢 ready for review; update after interviews |
| Architecture diagrams (context, use case, component) | 🟢 ready for review |
| UX prototype | 🟢 clickable Figma prototype (4 screens); user test with 3 people in progress |
| Verification and evaluation plan | 🟢 ready for review |
| Code | ⚪ not started (planned after pre-defense-1) |

_Update this table in every pull request that changes a stage._

## Selected technologies (proposed — see [technology comparison](docs/05-technology-comparison.md))

| Layer | Choice |
|---|---|
| Frontend | Next.js + React + TypeScript, Tailwind CSS |
| Backend | Python, FastAPI, SQLAlchemy, Alembic |
| Data | PostgreSQL + pgvector |
| Local LLM serving | Ollama (development), vLLM (production), OpenAI-compatible API |
| Models (to benchmark) | Qwen3, Gemma, Mistral Small families (final choice by measurement) |
| CI/CD and deployment | GitHub Actions, Docker Compose, Caddy |
| Testing | pytest, Vitest, Playwright, k6 |

Exact versions are pinned in dependency files once code exists.

## Links

- **Repository:** https://github.com/yssnov/ai-testcase-generator
- **Task board (Notion, approved by the supervisor instead of YouTrack):** `https://app.notion.com/p/3fe7cd9b361e801fa81cf78258ea88b9?v=f33259171f464d609c45bbcfd45932df&source=copy_link` ← replace
- **Prototype (Figma, clickable):** https://www.figma.com/design/m2NAfVfFTXCA4SMN7yZp5F
- **Documentation index:** [docs/README.md](docs/README.md)
- **Diagrams:** [diagrams/](diagrams/)

## Repository structure

```
.
├── docs/            proposal, evidence, reviews, comparisons, requirements, architecture, plans, feedback log
├── diagrams/        src/ (editable PlantUML) and export/ (SVG/PNG)
├── prototype/       wireframes (HTML sources + PNG exports) and UX notes
├── src/             backend/, frontend/, ai/  (code starts after pre-defense-1)
├── tests/           automated tests and test data
├── config/          configuration examples (no secrets)
└── .github/         pull request template, CI workflows
```

## Setup, run, test

_No runnable code yet. This section will contain:_ prerequisites, `cp config/.env.example .env`, `docker compose up`, how to run tests (`pytest`, `npm test`, `npx playwright test`).

## Workflow

Every change goes through a Notion task (ID `DIP-<n>`) → branch `feature/DIP-<id>-short-name` → pull request reviewed by another team member → merge to `main`. See [CONTRIBUTING.md](CONTRIBUTING.md).

## Pre-defense submissions

| Tag | Date | Summary | Known limitations |
|---|---|---|---|
| `pre-defense-1` | 2026-10-24 | Analysis, design and planning package | No application code yet |
