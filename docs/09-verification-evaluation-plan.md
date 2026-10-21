# 9. Verification and Evaluation Plan

The aim has two parts, and each needs its own evidence: (1) the system works as specified – verification against Section 6; (2) local-LLM generation is good enough to be useful – evaluation against baselines. Targets are pre-registered now and will not be changed after the results are known. Owners: Nuraly Abat – AI evaluation (9.3–9.6); Sultan Muratbek – performance, reliability, security (9.7); Kaisar Yessenov – test strategy, end-to-end tests, usability (9.2, 9.8).

## 9.1 What "Aim Achieved" Means

*Table 9.1 – Evidence for the project aim*

| Aim component | Demonstrated by | Pass condition |
|---|---|---|
| Working system | All Must requirements verified (9.2) + live demo of scenarios 1–4 | 100 % of Must acceptance criteria pass |
| Useful generation | Evaluation 9.3–9.6 | Proposed configuration P3 beats baseline B1 on coverage and acceptance rate (statistically) and meets NFR-AIQ targets |
| Practical value | User study 9.8 | Time to an accepted test suite lower than the manual baseline B0; SUS ≥ 68 |
| Production readiness | Load, reliability and security tests 9.7 | NFR-PERF, NFR-REL and NFR-SEC targets met |

## 9.2 Testing Plan (Verification)

*Table 9.2 – Test levels*

| Level | Scope | Tools | Gate |
|---|---|---|---|
| Unit | Parser, segmenter, prompt builder, validator, verifier, exporters; LLM replaced by a fake provider | Pytest, Vitest | ≥ 95 % line coverage of domain/service code |
| Contract | Same suite against each LLMProvider (Ollama, vLLM) and each exporter; API schema conformance | Pytest, Schemathesis | 100 % pass |
| Integration | API + real PostgreSQL: migrations, transactions, worker crash/retry, IDOR checks | Pytest, testcontainers | 100 % pass |
| End-to-end | Scenarios 1–4 in a browser with a fake LLM | Playwright | 100 % pass, < 5 min |
| Performance | Scenarios PERF-1…3 (9.7) | k6, Prometheus, Grafana | NFR-PERF targets |
| Security | Auth tests, upload negative tests, prompt-injection red-team set, dependency and container scans | Pytest, Trivy, pip-audit, npm audit, gitleaks, OWASP ZAP | No high/critical findings; NFR-SEC-04 passes |
| Acceptance | Each Must acceptance criterion mapped to a test ID or demo step | Traceability table | 100 % of Must |

All tests run in GitHub Actions on every pull request; merging requires a green pipeline.

## 9.3 Evaluation Dataset

**1. Documents.** 5–8 public requirements documents (PURE collection of public SRS documents and other public SRS), 1–2 documents from interviewees (with permission) and our own SRS; web, mobile and finance-like domains; English and Russian, Kazakh subset if available. The licence of each document is recorded.

**2. Size.** ≥ 60 requirements in total, of which ≥ 30 have gold test cases.

**3. Gold test cases.** Written independently by two team members using ISO/IEC/IEEE 29119-4 techniques; disagreements resolved by the third member; agreement reported as Cohen's κ.

**4. Splits.** A dev split for prompt design and few-shot examples, and a held-out test split used only for final runs.

**5. Red-team set.** 20 documents with hidden instructions (prompt injection) for NFR-SEC-04.

## 9.4 Baselines and Configurations

*Table 9.3 – Configurations compared*

| ID | Configuration | Role |
|---|---|---|
| B0 | Manual test design by a QA engineer or student (time and output recorded) | Human baseline (effort, quality) |
| B1 | Same local model, zero-shot prompt, no schema constraint, no RAG, no verifier | Technical baseline ("just ask the model") |
| P1 | Few-shot prompt + JSON-schema output | Ablation |
| P2 | P1 + RAG context | Ablation |
| P3 | P2 + verifier (duplicates, grounding) – proposed system | Main configuration |
| R | Large cloud model on public documents only, same prompt as P3 | Reference upper bound (optional; respects C-01) |

Models: three local open-weight families – Qwen3, Gemma and Mistral – in different sizes (8B to ~30B class); the final list is fixed after the GPU is confirmed. Each configuration × model is run 3 times with different seeds.

## 9.5 Outcome Metrics

*Table 9.4 – Primary metrics (pre-registered targets)*

| Metric | Definition | Target | Requirement |
|---|---|---|---|
| Schema-valid rate | % of generations that parse and validate within ≤ 2 retries | ≥ 95 % | NFR-AIQ-01 |
| Requirement coverage | % of requirements with ≥ 1 case judged valid | ≥ 80 % | NFR-AIQ-02 |
| Acceptance rate | % of generated cases a reviewer accepts with no or minor edits | ≥ 70 % and > B1 | FR-08 |
| Hallucination rate | % of cases with features, values or limits not present in the source requirement (labelled sample ≥ 100 cases, 2 raters, κ) | ≤ 10 % | NFR-AIQ-03 |
| Duplicate rate | % of cases with embedding similarity above a threshold to another case of the same requirement | ≤ 10 % | FR-07 |
| Invalid reference rate | % of cases citing non-existent requirement IDs (after the verifier) | 0 % | FR-06 |
| Time to accepted suite | Minutes to produce an accepted suite for 10 requirements (user study) | < B0 | Section 9.8 |

*Table 9.5 – Secondary metrics (reported, no target)*

| Metric | Definition | Why secondary |
|---|---|---|
| BLEU and ROUGE-L | n-gram overlap of generated cases with gold cases | Reported for comparability with L19, L22, L25; overlap can disagree with expert judgement (L19) |
| Gold recall | % of gold cases matched by a generated case (semantic similarity + manual check) | Method of L11; depends on the gold set |
| G-Eval score | LLM-as-judge rating of semantic correctness on a rubric, run with a local judge model | Automatic; calibrated against human ratings on a sample |
| Quality rubric | 1–5 ratings of relevance, correctness, coherence, feasibility (≥ 2 raters) | Method of L7; costly, used on a sample |
| Latency and throughput | Time to first token, batch time p50/p95, tokens/s at 1/5/10 parallel jobs, VRAM; Ollama vs vLLM | Engineering metric (NFR-PERF-03) |
| Cost | Cost per 1 000 cases: local GPU (amortised + electricity) vs cloud API list price | Supports the on-premise argument |

## 9.6 Measurement Conditions and Analysis

**1. Recorded for every run:** GPU model and VRAM, driver, runtime and version, model name and exact revision, quantisation, context length, temperature (0–0.3), seed, prompt version (Git commit).

**2. Reproducibility:** each run is a configuration file; raw results are stored as CSV/JSON with the commit hash; tables in the thesis are produced by scripts.

**3. Statistics:** paired comparisons on the same requirements with the Wilcoxon signed-rank test (Friedman for more than two configurations); effect sizes and 95 % confidence intervals; inter-rater agreement with Cohen's κ.

**4. Threats to validity:** small dataset and few raters, domain bias of public SRS, prompt over-fitting to the dev split, non-determinism across hardware and quantisation, fast-changing model versions.

## 9.7 Performance, Reliability and Security Scenarios

*Table 9.6 – Scenarios and pass criteria*

| ID | Scenario | Conditions | Pass |
|---|---|---|---|
| PERF-1 | Browse mix: login, list, open document, filter cases | 50 virtual users, 10 min, production-like server | p95 < 300 ms; errors < 1 % |
| PERF-2 | Generation burst | 10 parallel jobs every 10 s for 15 min on the reference GPU | Queue wait p95 < 30 s; job p95 < 90 s |
| PERF-3 | Soak test | 2 h at average load (≈ 2 000 jobs/day rate) | No memory growth, no connection leaks |
| REL-1 | Kill the worker mid-job | 20 trials | 0 lost jobs, 0 partial results |
| REL-2 | Backup restore drill | Nightly dump restored to a clean server | < 30 min |
| SEC-1 | Prompt-injection red-team set | 20 documents | Output schema-valid; no injected instruction followed |
| SEC-2 | IDOR / authorisation tests on every endpoint | Two users | 0 unauthorised accesses |
| SEC-3 | Egress check in production | Network monitoring during PERF-2 | No calls to external AI APIs |

## 9.8 User Study (Usability and Effort)

**1. Participants:** ≥ 5 QA engineers or senior Software Engineering students (interviewees from Section 2 are invited first).

**2. Task:** produce an accepted test suite for 10 requirements, once manually (B0) and once with the system, in counter-balanced order on different but comparable requirement sets.

**3. Measures:** time to completion, number of accepted cases, errors found by a second reviewer, SUS questionnaire, short interview.

**4. Ethics:** consent form, anonymised results.

## 9.9 Evaluation Timeline

*Table 9.7 – Evaluation timeline*

| When | What |
|---|---|
| November 2026 | Dataset and gold cases; evaluation harness skeleton; baseline B1 on one model |
| December 2026 | Benchmark round 1: 3 models × B1, P1; model shortlist (D6) |
| February–March 2027 | Full runs P1–P3 (+ R), ablations, statistics; PERF / REL / SEC tests on the production setup |
| April 2027 | User study; final tables for the thesis |
