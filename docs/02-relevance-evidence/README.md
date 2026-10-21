# 2. Evidence of Relevance

Requirement for pre-defense 1: 3–5 discussions with representatives of potential users, with verified findings clearly separated from assumptions. Status on the report date: interviews are scheduled; the hypotheses below are still assumptions unless supported by literature. Results will be added to Sections 2.4–2.5 and to the repository (docs/02-relevance-evidence) after the interviews, target date 22 October 2026.

## 2.1 Interview Plan

*Table 2.1 – Interviewee profiles and interviewers*

| # | Interviewee profile | Why this profile | Interviewer | Date | Status |
|---|---|---|---|---|---|
| P1 | QA engineer / test analyst, 2+ years | Primary user: writes test cases from requirements | Nuraly Abat | __.10.2026 | Planned |
| P2 | QA engineer / test analyst | Second primary user, different company or domain | Sultan Muratbek | __.10.2026 | Planned |
| P3 | QA lead or test manager | Owns coverage, traceability and tool choice | Kaisar Yessenov | __.10.2026 | Planned |
| P4 | Business / system analyst | Writes the requirements; judges quality flags | Kaisar Yessenov | __.10.2026 | Planned |
| P5 | Developer or lead in an organisation with a restricted AI policy (bank, public sector, telecom) | Checks the data-restriction hypothesis (H3) | Sultan Muratbek | __.10.2026 | Planned |

## 2.2 Method

**1. Format.** Structured interview in an online chat (Telegram, WhatsApp or LinkedIn); 5 open questions about past experience, sent one at a time, with follow-ups built into each question: Q1 what took most time last week and what was most tedious; Q2 the last tested feature (requirements source, form, language, hours, tools); Q3 the last escaped bug or rework; Q4 AI or other tools tried, company rules and who decides; Q5 what the respondent has already tried to simplify.

**2. No product pitch, no leading questions.** The aim is to find the most painful or tedious part of QA work, which may differ from our topic. Our idea is described only after all questions, if the respondent asks. Questions about future intentions ("would you use…?") are not asked, because they produce polite agreement rather than evidence.

**3. Consent and privacy.** Consent is obtained in the chat before the questions. Chat logs and raw notes are stored outside Git; only anonymised notes (P1–P5, role, industry, years of experience) are committed.

**4. Facts vs opinions.** Within 24 hours each interviewer writes notes from the template and marks every statement as fact (what actually happened) or opinion (what the person thinks or would like).

**5. Pains outside our topic.** If the respondent names a pain unrelated to test design (regression, test data, environments, reporting), it is explored and recorded in full; such findings may change the requirements.

## 2.3 Hypotheses and Current Status

Status values: VERIFIED – supported by at least 3 of 5 interviews or by data; PARTIAL – supported by literature or by fewer interviews; REFUTED – contradicted (the affected requirement must be changed); ASSUMPTION – not yet checked.

*Table 2.2 – Hypotheses, evidence and affected requirements*

| ID | Hypothesis (assumption) | Questions | Evidence so far | Status | Requirements affected |
|---|---|---|---|---|---|
| H1 | Writing test cases from requirements takes a significant share of QA time (industry estimate 30–40 %) | Q1, Q2 | Industry estimate only; no data for our target teams | ASSUMPTION | FR-05, NFR-PERF-03 |
| H2 | Requirements are often left without test cases; gaps are found late | Q3 | Not yet collected | ASSUMPTION | FR-09 (traceability, coverage) |
| H3 | Regulated organisations restrict sending requirement documents to external AI services | Q4 | Not yet collected; cloud-only status of tools E2, E3 confirmed (Section 4) | ASSUMPTION | Constraint C-01, NFR-PRIV-01 |
| H4 | Vague or incomplete requirements reduce the quality of generated tests | Q3 | Literature: effectiveness drops for vague requirements [L12]; low-quality requirements are a known obstacle [L6, L27] | PARTIAL | FR-04 (quality gate) |
| H5 | Users accept AI drafts only with a review step and a visible link to the requirement | Q4 (indirect) | Literature: correctness rated lower than coherence [L7]; all commercial tools keep a review step (Section 4) | PARTIAL | FR-06, FR-08 |
| H6 | Required export formats are spreadsheets (CSV/XLSX) and test-management tools (Jira/Xray, TestRail, Qase) | Q2 | Not yet collected | ASSUMPTION | FR-10, FR-11 |
| H7 | Requirements are written in Russian and English; Kazakh less often | Q2 | Not yet collected | ASSUMPTION | NFR-LANG-01, NFR-LANG-02 |
| H8 | Test design from requirements is among the most painful or tedious parts of QA work (respondents name it without prompting) | Q1, Q5 | Not yet collected; open question, may be refuted | ASSUMPTION | Project focus; if refuted, re-scope with the supervisor |

## 2.4 Synthesis of Findings

To be completed after the interviews. Each finding will name the interviews that support it, its type (VERIFIED / PARTIAL / REFUTED) and the resulting change in the requirements specification (Section 6, column "Source").

*Table 2.3 – Synthesis of interview findings (template)*

| Finding | Supported by | Type | Consequence for requirements |
|---|---|---|---|
| To be filled after the interviews | — | — | — |

## Materials

- [Interview guide (EN)](interview-guide.md) · [Гайд интервью (RU)](interview-guide-ru.md)
- [Notes template](interview-notes-template.md) · [Consent text](consent-form.md)
- Anonymised notes: `notes/P1.md` … `notes/P5.md` (chat logs and raw notes stay outside Git)
