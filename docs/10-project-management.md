# 10. Project management and risks

**Committee question:** are project activities traceable, and are the next steps clearly defined?

- **Task tracker:** Notion database "Tasks", IDs **DIP-<n>** (38 tasks). Notion is used instead of YouTrack with the supervisor's approval of 19 Oct 2026: https://app.notion.com/p/3fe7cd9b361e801fa81cf78258ea88b9?v=f33259171f464d609c45bbcfd45932df
- **Board:** Notion board view grouped by Status: Open → In Progress → In Review → Done. Each closed task links to the pull request that delivered it.
- **Repository:** https://github.com/yssnov/ai-testcase-generation. `main` is protected (pull request + 1 approval). Workflow rules are in [CONTRIBUTING.md](../CONTRIBUTING.md).
- **Traceability rule:** task `DIP-n` → branch `feature/DIP-n-<name>` → commits `DIP-n: ...` → pull request reviewed by another member → merge into `main`.

## 10.1 Allocation of responsibilities

R = responsible (does the work), A = accountable (approves), C = consulted (reviews).

| Deliverable / area | Nuraly (A-role, AI) | Sultan (B-role, backend) | Kaisar (C-role, frontend/QA) | Supervisor |
|---|---|---|---|---|
| Repository skeleton, README | C | C | R (DIP-1, DIP-3) | — |
| Notion task board | R (DIP-2) | C | C | A |
| 01 Proposal & scope | R (DIP-5) | C | C | A |
| 02 Interview materials | C | R (DIP-4) | C | A |
| 02 Interviews | R (P1) | R (P2, P5) | R (P3, P4) | C |
| 02 Evidence synthesis | C | C | R (DIP-22) | A |
| 03 Literature review | R (lead, DIP-8; 9 sources) | R (6 sources) | R (6 sources) | A |
| 04 Existing systems | C | C | R (DIP-9) | A |
| 05 Technology comparison, ADRs | R (ADR-0002, DIP-13) | R (D2–D4, ADR-0001/3/4, DIP-6) | R (D5) | A |
| 06 Requirements | R (AI requirements) | R (lead, DIP-26; NFR perf/rel/sec) | R (UX and usability) | A |
| 07 Architecture and diagrams | R (AI part) | R (context, component, DIP-24) | R (use case, DIP-17) | A |
| 08 UX prototype (Figma) | C | C | R (DIP-27) | A |
| 09 Verification & evaluation plan | R (lead, DIP-28) | R (9.7) | R (9.2, 9.8) | A |
| 10 Project management, risks | R (DIP-32) | R (risks, GPU plan, DIP-31) | C | A |
| 11 Feedback log | C | C | R (DIP-10) | A |
| Tag and submission summary | C | C | R (DIP-37) | — |
| Pre-defense slides | R (own part) | R (own part) | R (own part) | C |

Each pull request is reviewed by another member: Nuraly → Kaisar, Sultan → Nuraly, Kaisar → Sultan.

Code ownership after pre-defense-1: S1 generation and evaluation — Nuraly; S2 import, data, DevOps — Sultan; S3 review, export, UI, QA — Kaisar.

## 10.2 Progress at pre-defense-1 (state on 22 Oct 2026)

| Member | Merged pull requests | Tasks |
|---|---|---|
| Kaisar Yessenov | 6 | DIP-1, DIP-3, DIP-9, DIP-17, DIP-22, DIP-27 |
| Nuraly Abat | 4 | DIP-5, DIP-8, DIP-13, DIP-28 |
| Sultan Muratbek | 4 | DIP-4, DIP-6, DIP-24, DIP-26 |

## 10.3 Milestones

| ID | Planned date | Milestone | Status on 22 Oct | Evidence |
|---|---|---|---|---|
| M0 | 2026-10-10 | Repository, branch protection, task tracker, access for supervisor | Done late (tracker switched to Notion on 19 Oct; repository recreated) | README, Notion board |
| M1 | 2026-10-15 | Drafts: proposal, literature, existing systems, technology comparison | Done (merged 20–21 Oct) | PRs DIP-5, DIP-8, DIP-9, DIP-6 |
| M2 | 2026-10-20 | Interviews synthesised; requirements; 3 diagrams; Figma prototype; verification plan | Partly done: documents merged; interviews in progress | PRs DIP-26, DIP-24, DIP-17, DIP-27, DIP-28 |
| M3 | 2026-10-22 | Supervisor review of the full package | Done: no comments (see 11) | docs/11 |
| M4 | 2026-10-23 | Interview notes and synthesis; tag `pre-defense-1`; slides rehearsed | Planned | Tag on GitHub |
| PD1 | 2026-10-24 | **Pre-defense 1** | — | — |
| M5 | 2026-12 | First end-to-end generation; dataset with gold cases; benchmark round 1 | Planned | Demo, evaluation report |
| M6 | 2027-01-31 | MVP (all Must requirements) on staging | Planned | Demo, CI green |
| PD2 | TBA (department) | Pre-defense 2, tag `pre-defense-2` | — | — |
| M7 | 2027-03 | Full experiments, load and security tests, deployment | Planned | Reports |
| FPD | TBA (department) | Final pre-defense, tag `final-pre-defense` | — | — |
| D | 2027-05/06 | Defense (per academic calendar) | — | — |

**Deviation from plan:** M0–M2 slipped by about one week because the task tracker was changed and the repository was recreated. Interviews (component 2) are the main open item before pre-defense-1.

## 10.4 Risks

| ID | Risk | Probability | Impact | Mitigation | Owner | Trigger |
|---|---|---|---|---|---|---|
| R1 | No GPU available for the local LLM | Medium | High | Confirm team GPU or request university resources by 31 Oct; develop with small models; short paid GPU rental for the load test | Sultan | No GPU by 31 Oct |
| R2 | Too few interviewees | High | High (component 2) | Online chat interviews; QA communities and personal contacts in different companies; minimum 3, target 5 | All | < 3 interviews by 23 Oct |
| R3 | Local models produce low-quality cases | Medium | High | Quality gate, verifier, RAG, few-shot; compare 3–4 models; report results honestly | Nuraly | Coverage < 60% in round 1 |
| R4 | Scope creep (integrations, fine-tuning) | High | Medium | MoSCoW in 06; supervisor approves new scope | Nuraly | New feature request |
| R5 | Uneven contribution / last-minute commits | Medium | High (assessment) | Tasks per person in Notion; small PRs; weekly check of the contribution graph | All | A member with no merged PR in a week |
| R6 | Literature summarised without reading | Medium | Medium | Each owner rewrites the appraisal of own sources in own words (DIP-11, DIP-12, DIP-23) | Nuraly | Appraisal not revised by owner |
| R7 | Secrets or personal data committed | Low | High | `.gitignore`, anonymised interview notes only, chat logs kept outside Git | Sultan | Secret or name found in a PR |
| R8 | Dataset licence or permission problems | Low | Medium | Public documents with known licence only | Nuraly | Unknown licence |
| R9 | Competitor features misreported | Medium | Medium | "Not stated" cells confirmed from vendor documentation or trials before pre-defense 2 | Kaisar | Committee question without evidence |

## 10.5 Dependencies

| ID | Dependency | Needed for | Needed by | Status |
|---|---|---|---|---|
| D-01 | GPU host (≥ 12 GB VRAM, Linux for vLLM) | Generation, benchmark | Nov 2026 | Open: plan to be confirmed by 31 Oct |
| D-02 | Interviewees (3–5) | Component 2, requirements | 23 Oct 2026 | In progress |
| D-03 | Notion workspace and access for supervisor/committee | Component 10 | 10 Oct 2026 | Done |
| D-04 | Public requirements documents with licences | Dataset (09) | Nov 2026 | Open |
| D-05 | Supervisor review | Component 11 | 22 Oct 2026 | Done |
| D-06 | Department dates for pre-defense 2 and final | Planning | — | Waiting |

## 10.6 Next steps after pre-defense-1

1. Log committee comments in 11 and fix each one in its own pull request.
2. Confirm the "Not stated" cells in 04 and the GPU plan (R1, R9).
3. Code skeleton: backend, frontend, worker, CI pipeline.
4. Dataset with gold cases, evaluation harness, baseline B1.
5. First vertical slice of each member (S1, S2, S3) end to end with a fake LLM, then with the real model.
