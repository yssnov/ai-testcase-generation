# 4. Existing System Comparison (Benchmarking)

Five systems were compared against nine criteria applied consistently. Cells are based on the vendors' public pages checked on 8 October 2026 (evidence list in 4.3). "Not stated" means that the checked public sources do not mention the feature; it does not mean the feature is absent. These cells will be confirmed through trials or demos before pre-defense 2.

## 4.1 Systems Selected

*Table 4.1 – Compared systems*

| ID | System | Why it is relevant |
|---|---|---|
| E1 | Xray (Jira app) – AI Test Case Generation | Widely used Jira test management app; AI generation from Jira requirements announced in October 2025 |
| E2 | TestRail – AI Test Case Generation | Popular test management tool; AI generation released in TestRail 9.5 (September 2025) |
| E3 | Qase – AI Test Case Generator (AIDEN) | Test management SaaS with AI generation from requirement text or Jira/GitHub issues |
| E4 | Tricentis qTest – Copilot | Enterprise test management with AI generation from requirements |
| E5 | General-purpose LLM chat (e.g. ChatGPT) used manually | What QA engineers do today without a dedicated tool (practical baseline) |

## 4.2 Comparison

*Table 4.2 – Comparison, part 1 (E1–E3)*

| Criterion | E1 Xray AI | E2 TestRail AI | E3 Qase AI |
|---|---|---|---|
| C1. Input | Written requirements, preconditions, Jira issues [x1] | Requirements text entered by the user [t1] | Title + description, or Jira Cloud / GitHub issue ID [q1] |
| C2. Output | Manual and Cucumber-style tests [x1] | Test cases with steps and expected results; BDD field mapping [t1, t2] | Manual test cases saved to a suite [q1] |
| C3. Traceability to requirements | Generated from Jira requirement issues [x1]; link details not stated | Not stated on AI feature pages [t1, t2] | Shows the issue IDs used as input [q1] |
| C4. Human review before saving | Yes – review and select suggestions [x1] | Yes – review, edit, select [t2] | Yes – review, delete, save or send to review [q1] |
| C5. Where the model runs | Xray Cloud; Data Center: not stated [x1] | TestRail Cloud only [t1] | Vendor cloud; Beta uses the ChatGPT API platform [q1] |
| C6. Data handling statement | "Encrypted in transit and never stored or used to train the model" [x1] | Not stated on checked pages [t1] | Data not used to train the model [q1] |
| C7. Explicit test design techniques | Not stated | Not stated | Not stated |
| C8. Russian / Kazakh requirements | Not stated | Output follows the input language [t1] | Not stated |
| C9. Availability / cost | Paid Jira app; generation in Advanced/Enterprise editions [x1] | Commercial; AI audit logs are an Enterprise feature [t1] | Commercial SaaS; feature in Beta, admin can disable [q1] |

*Table 4.3 – Comparison, part 2 (E4, E5 and the proposed system)*

| Criterion | E4 qTest Copilot | E5 LLM chat (manual) | Proposed system |
|---|---|---|---|
| C1. Input | Requirements and images [c1] | Pasted text or uploaded file | SRS/PRD documents (PDF, DOCX, MD) with automatic requirement extraction |
| C2. Output | Test assets / test cases [c1] | Free text; structure depends on the prompt | Schema-validated cases (steps, expected results, data, technique, priority); Gherkin, CSV, XLSX, JSON export |
| C3. Traceability to requirements | Described as traceable [c1] | None | Every case cites ≥ 1 existing requirement ID; traceability matrix and coverage % |
| C4. Human review before saving | Not described in detail [c1] | Manual copy-paste | Mandatory accept / edit / reject per case; decisions logged |
| C5. Where the model runs | Not stated [c1] | Vendor cloud | Organisation's own server (local open-weight model) |
| C6. Data handling statement | Not stated [c1] | Depends on plan and settings; data leaves the organisation | Documents never leave the organisation's infrastructure |
| C7. Explicit test design techniques | Not stated | Only if the user asks in the prompt | Technique selected and recorded per case (ISO/IEC/IEEE 29119-4) |
| C8. Russian / Kazakh requirements | Not stated | Supported by most large models; quality varies | EN and RU evaluated; KK as a measured stretch goal |
| C9. Availability / cost | Commercial enterprise product [c1] | Free and paid plans | Self-hosted; hardware cost only |

## 4.3 Evidence (checked 8 October 2026)

[x1] Xray launches AI-powered, human-guided test capabilities with Sembi IQ (announcement, 9 Oct 2025): https://martechseries.com/predictive-ai/ai-platforms-machine-learning/xray-launches-ai-powered-human-guided-test-capabilities-with-sembi-iq/ (to be replaced by Xray product documentation).

[t1] TestRail Support, "Quick Start: Generate Test Cases with AI": https://support.testrail.com/hc/en-us/articles/37119835854484

[t2] TestRail blog, "Introducing TestRail 9.5" (11 Sep 2025): https://www.testrail.com/blog/testrail-9-5/

[q1] Qase documentation, "AI Test Case Generator": https://docs.qase.io/qase-ai

[c1] Tricentis qTest Copilot product page: https://tricentis.com/products/unified-test-management-qtest/copilot ; launch news (7 Nov 2024): https://sdtimes.com/ai/tricentis-launches-qtest-copilot/

## 4.4 Conclusion

Commercial test-management tools already generate test cases from requirements, and all of them that document the workflow keep a human review step. Therefore "AI generates test cases" alone is not a novelty of this project. The gap addressed is narrower:

**1. Self-hosting.** No self-hosted model option is stated for E1–E4 in the checked sources; E2 is explicitly cloud-only and E3 sends data to a cloud LLM API. Organisations that forbid external AI services (H3) cannot use them.

**2. Document-level input.** Uploading a whole SRS with automatic requirement extraction is not stated for E1–E3, which work from requirement text or tracker issues.

**3. Measurable quality.** Explicit test design techniques and published quality metrics (coverage, duplicates, hallucinations) are not documented for any of the tools.

**4. Language.** Russian and Kazakh support is not documented, except E2 following the input language.

Limitation stated honestly: mature tools offer integrations, scale and support that a diploma MVP will not match. The proposed system does not replace them; it exports to their import formats (FR-11).
