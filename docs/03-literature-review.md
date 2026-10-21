# 3. Literature Review and Research Gap

The review uses **27 scientific publications** (20 peer-reviewed journal and conference papers, 7 preprints) and **3 standards / industry documents** (S1–S3), which are listed separately and are not counted as scientific sources. 24 of the 27 publications are from 2021–2026; three earlier works (L1, L2, L15) are kept as foundational. This exceeds the department minimum of 12 sources with at least 8 scientific publications.

## 3.1 Search Protocol

**1. Databases.** Google Scholar, arXiv, IEEE Xplore, ACM Digital Library, Scopus (university access), OpenAlex, Scientific Journal of Astana IT University.

**2. Queries.** "test case generation" AND (requirements OR SRS OR "user stories") AND (LLM OR "large language model" OR NLP); "retrieval-augmented" AND testing; "local" OR "open-weight" LLM AND testing.

**3. Inclusion.** Generation of tests from natural-language requirements or user stories; 2021–2026 except foundational works; English or Russian. Supporting topics: RAG, LLM serving, hallucination, prompt injection, small/fine-tuned models.

**4. Exclusion.** Unit-test generation from source code only, unless used for method comparison (L22).

**5. Local sources.** 291 records of the AITU journal were scanned; none addresses test-case generation, so the three closest papers on RAG and small or fine-tuned models were included (L19–L21). A search of eLibrary and CyberLeninka for Russian/Kazakh sources is in progress.

## 3.2 Structured Analysis of Publications

Type: J – journal, C – peer-reviewed conference, P – preprint, S – standard or industry guidance. Journal quartiles for L5 and L22–L27 are taken from SCImago for the year of publication.

*Table 3.1 – Publications: approach, data and key findings*

| ID | Reference (short) | Year | Type | Approach and data | Key findings |
|---|---|---|---|---|---|
| L1 | Garousi, Bauer, Felderer – NLP-assisted software testing: systematic mapping | 2020 | J | Systematic mapping of NLP use in testing; published literature | Maps how NLP supports test generation from textual artefacts (pre-LLM) |
| L2 | Wang, Pastore, Göknil, Briand – Acceptance test cases from use case specifications (UMTG) | 2020 | J | NLP + restricted use-case language → executable acceptance tests; industrial case studies | Automated generation is feasible when requirements follow a restricted template |
| L3 | Zhao et al. – NLP for Requirements Engineering: systematic mapping | 2021 | J | Mapping study of NLP4RE research | Overview of NLP tasks on requirements; large gap between research tools and industrial use |
| L4 | Mustafa et al. – Automated test case generation from requirements: SLR | 2021 | J | Systematic literature review | Classifies requirement-based generation approaches and their limitations |
| L5 | Wang J. et al. – Software testing with LLMs: survey, landscape, vision (IEEE TSE, Q1) | 2024 | J | Survey of 102 studies on LLMs in software testing | Maps testing tasks where LLMs are used (mostly unit tests, program repair) and open challenges |
| L6 | Yang, Huang, Cui, Niu, Towey – Requirements-based test generation: comprehensive survey | 2025 | P | Survey of 267 studies (1994–2024) | Open problems: low-quality requirements, gap between abstract and executable tests, no standard benchmarks, weak industrial adoption |
| L7 | Arora, Herda, Homm – Test scenarios from NL requirements with retrieval-augmented LLMs (RAGTAG) | 2024 | P | RAG + GPT-3.5/GPT-4, 8 configurations; bilingual (German/English) requirements, Austrian Post | Few-shot + retrieval worked best; experts rated coherence high but correctness lower |
| L8 | Korraprolu, Pinninti, Reddy – Test case generation for NL requirements: LLM comparison | 2025 | C | 6 LLMs incl. Llama 3; technical requirements checked against a Simulink model | Coverage-based quantitative comparison of LLMs is feasible |
| L9 | Bhatia, Gandhi, Kumar, Jalote – System test case design from SRS with ChatGPT | 2024 | P | Prompt chaining, GPT-4o; SRS of 5 student projects rated by their developers | ≈87.7 % of cases valid (15.2 % new to developers); ≈2.6 % redundant; ≈9.7 % not applicable |
| L10 | Ferreira, Viegas, Faria, Lima – Acceptance test generation with LLMs: industrial case study (IEEE/ACM AST 2025) | 2025 | C | GPT-4 Turbo: user stories → Gherkin → Cypress tests; automotive company | 95 % of scenarios helpful; 60 % of executable tests usable as is, 92 % after minor fixes |
| L11 | Masuda et al. – High-level test cases from requirements using LLM: industry study | 2025 | P | Prompt-only: derive test design techniques, then cases; Bluetooth and Mozilla datasets | Macro-recall vs reference cases 0.81 (Bluetooth) and 0.37 (Mozilla) |
| L12 | Kogler et al. – RESTestBench: LLM-generated REST API tests from NL requirements | 2026 | P | Benchmark with precise vs vague requirements and mutants; 10 LLMs; 3 REST services | Effectiveness drops for vague requirements; naive refinement loops can make results worse |
| L13 | Moradi, Yan, Colwell, Asgari – LoRA fine-tuning of LLMs for test case generation | 2026 | P | LoRA fine-tuning of open models (DeepSeek, Llama-3.1-8B, Ministral-8B) vs GPT-4.1; industrial lab (Tricentis) | Fine-tuning improved all open models; fine-tuned 8B approached un-tuned GPT-4.1 |
| L14 | Folorunsho, Reza – AI-driven test case generation from NL requirements: survey of techniques and gaps | 2026 | P | Survey of 26 primary studies (2000–Oct 2025) | No approach covers automation, ambiguity handling, domain applicability, traceability, thorough evaluation and hallucination control together |
| L15 | Lewis et al. – Retrieval-augmented generation for knowledge-intensive NLP | 2020 | C | RAG architecture; open-domain QA benchmarks | Retrieval grounds generation and improves factuality |
| L16 | Kwon et al. – Efficient memory management for LLM serving with PagedAttention (vLLM) | 2023 | C | PagedAttention, continuous batching; serving benchmarks | Higher throughput than earlier serving systems at the same latency |
| L17 | Greshake et al. – Indirect prompt injection in LLM-integrated applications | 2023 | C | Attack taxonomy and demonstrations on real applications | Instructions hidden in retrieved or uploaded content can hijack the model |
| L18 | Ji et al. – Survey of hallucination in natural language generation | 2023 | J | Survey of NLG tasks | Taxonomy, metrics and mitigation of hallucination |
| L19 | Tugambayeva, Sakhipov – AI-based question generation for aviation training: RAG vs fine-tuned models (Sci. J. AITU) | 2026 | J | RAG (FAISS + Mistral-7B, 238 documents) vs LoRA-tuned T5-small (920 pairs); 116 test examples; expert rating, BLEU, ROUGE-L, BERTScore | RAG: broader terminology coverage (92.2 % vs 44.0 %), more diverse and higher-level questions; fine-tuned: higher similarity scores and ≈5× faster |
| L20 | Kapizov, Kumar – Fine-tuning small language models (PEFT) outperforming zero-shot LLMs (Sci. J. AITU) | 2026 | J | LoRA on SmolLM2-1.7B, two Reddit benchmarks; paired comparison with zero-shot GPT-4o-mini and GPT-4o; McNemar test | Small tuned model matched or beat the zero-shot cloud models; advantage significant on one of two datasets |
| L21 | Mansurova, Nugumanova, Makhambetova – Question answering chatbot for the blockchain domain (Sci. J. AITU) | 2023 | J | LLM + vector database (LangChain) + web retrieval; Kazakhstan fintech context | Connecting an LLM to an external knowledge base is promising for domain-specific tasks without retraining |
| L22 | Rehan, Al-Bander, Al-Said Ahmad – Harnessing LLMs for automated software testing (Electronics, Q2) | 2025 | J | QLoRA fine-tuned Llama-2-7B; Java unit tests from methods2test; human review of 52 cases | F1 ≈ 34 %, BLEU 7.48 %; ≈30 % of reviewed tests near-duplicates, ≈20 % with hard-coded values |
| L23 | Al-Azzoni, Iqbal, Al Ashkar, Erum – MDE and LLMs for test scenario generation for smart contracts (Information, Q2) | 2025 | J | LLM inside a model-driven pipeline; RBAC models as specification; tests translated to DAML | LLM-guided generation from a formal specification is feasible and can improve coverage and reduce manual effort |
| L24 | Mateus, Silveira, Araujo – User stories and Gherkin scenarios from BPMN models (Applied Sciences, Q2) | 2025 | J | Pattern-based (rule) transformation BPMN → user stories → Gherkin; tool; 5 experts, 4 models | Experts found the output useful (relevance 4.6/5, satisfaction 4.4/5); 3 of 13 user stories had errors |
| L25 | Boukhlif, Kharmoum, Hanine – Retrieval-augmented LLMs for test-case generation from SRS (IJIES, Q3) | 2026 | J | RAG (MiniLM) + few-shot examples from 8 sectors; GPT-4o and open models via Ollama (mistral:7b … llama3.3:70b); BLEU + expert ratings; ablation | Full system beat baseline prompting; GPT-4o BLEU 0.72, 4.8/5; mistral:7b BLEU 0.52, 3.55/5; few-shot examples were critical |
| L26 | Antonio, Alfredo, Gustavo – Prompt-orchestrated LLM workflows for test-case generation in agile (IJACSA, Q3) | 2025 | J | Dual-LLM (Gemini 1.5 + GPT-4) with schema-aware prompts; 50 user stories → 197 test cases; BDD output | ≈80 % less manual design effort; expert rating 4.75/5; 91.9 % functional correctness of BDD scripts |
| L27 | Intana, Tantayakul, Laosen, Charoenreh – Test case generation with software requirement ontology (IJACSA, Q3) | 2023 | J | Controlled natural language → OWL ontology → data dictionary → equivalence + classification-tree method; 2 case studies | Precision 100 %; recall 53.3 % (library system) and 100 % (diagnosis subsystem) |
| S1 | ISO/IEC/IEEE 29148:2018 – Requirements engineering | 2018 | S | Standard | Characteristics of good requirements (unambiguous, verifiable, complete …) |
| S2 | ISO/IEC/IEEE 29119-4:2021 – Test techniques | 2021 | S | Standard | Defines equivalence partitioning, boundary values, decision tables, state transitions |
| S3 | OWASP Top 10 for LLM Applications (2025) | 2025 | S | Industry guidance | Prompt injection, insecure output handling and other LLM risks |

*Table 3.2 – Relevance to the project and critical appraisal*

| ID | Relevance to our project | Critical appraisal (limitations) |
|---|---|---|
| L1 | Baseline of pre-LLM approaches | Useful taxonomy, but it predates LLMs and does not measure generation quality itself. |
| L2 | Shows the cost of structured input; our system must accept free-form SRS | Strong industrial validation, but the restricted language has to be written by hand, which is rare in practice. |
| L3 | Background for segmentation and quality checks | Broad and well cited, but descriptive only; it does not compare techniques empirically. |
| L4 | Pre-LLM state of the art for the comparison of approaches | Pre-LLM; quality of the included studies varies and is not weighted in the conclusions. |
| L5 | Positions our work in LLM-for-testing research | Most studies in it are code-level and use cloud models; requirements-to-test-case generation is a small part. |
| L6 | Justifies the quality gate, our gold dataset and the user study | Very broad, but a preprint (not yet peer reviewed); we treat its conclusions as indicative. |
| L7 | Supports RAG + few-shot + mandatory review; bilingual setting is similar to RU/EN | Closest to our setting, but one company, cloud models and a small expert panel; we test whether it holds for local models. |
| L8 | Model-comparison design; coverage as a metric | Embedded/control domain differs from information systems; venue details still to be confirmed. |
| L9 | Expected quality range; need for duplicate detection | Small sample, and ratings by the authors of the same projects may be optimistic. |
| L10 | Gherkin export; value of human-in-the-loop | Single industrial case and a cloud model; executable scripts are outside our scope. |
| L11 | Semantic-similarity evaluation against gold cases | Results depend strongly on the dataset; similarity metrics need a manual check, which we add. |
| L12 | Motivates the quality gate and a limit on retries | Strong design, but REST APIs only and a preprint. |
| L13 | Evidence that local 8B-class models can be competitive | Industrial data is not public; fine-tuning needs labelled data, so for us it is an optional path. |
| L14 | Our design targets traceability, ambiguity handling and hallucination control | Only 26 primary studies and a preprint; we cross-check its gap statement with L6. |
| L15 | Foundation of the RAG step | Evaluated on QA, not testing; the benefit for test generation must be measured (ablation P1 vs P2). |
| L16 | Justifies vLLM for the production load target | Measured on data-centre GPUs; we measure throughput on our own hardware. |
| L17 | Uploaded SRS files are untrusted input | No complete defence exists; we measure resilience on a red-team set instead of claiming immunity. |
| L18 | Definition of our hallucination metric | General NLG, not testing-specific; we adapt the definition to invented features, values or limits. |
| L19 | Shows that BLEU/ROUGE can disagree with expert judgement; supports RAG with a local 7B model | Different domain (education) and a small test set; therefore BLEU/ROUGE-L are only secondary metrics in our plan. |
| L20 | Small local models can be competitive while data stays local; example of paired statistical testing | Classification, not generation; paired subsets of only 200 examples. |
| L21 | Local example of a vector-DB RAG architecture (cf. pgvector design) | Results are preliminary; it relies on a cloud LLM and internet retrieval, unlike our on-premise constraint. |
| L22 | Small local models produce duplicates → verifier and duplicate metric | Unit tests from code, not requirements; older model; small human review. |
| L23 | Supports structured guidance of the model (requirement IDs, techniques, JSON schema) | Narrow domain and model-based input instead of NL documents; evaluation is mainly a feasibility study. |
| L24 | Gherkin as a target format; non-LLM alternative | Qualitative evaluation only (no precision/recall); requires BPMN models as input. |
| L25 | Closest architecture to ours (RAG + few-shot + Ollama); shows the gap between 7B and larger models | BLEU vs reference cases is weak for test cases; no traceability or schema validation; English only. |
| L26 | Supports schema-grounded prompting, Gherkin output and an effort baseline (B0) | Cloud models (conflict with our constraint); one dataset of 50 stories. |
| L27 | Clarifying requirements before generation improves results (quality gate); explicit test techniques | Semi-automatic: requirements must be rewritten manually in a controlled language; two small case studies. |
| S1 | Checklist of the quality gate | Normative; does not define automatic checks – we derive them. |
| S2 | Techniques the generator applies and labels | Normative; used as the vocabulary for the technique field. |
| S3 | Security requirements and tests | Grey literature; used for threat coverage, not as scientific evidence. |

## 3.3 Critical Review

**Pre-LLM approaches (L1–L4, L24, L27).** Earlier work generated tests through NLP pipelines, ontologies, rule-based patterns or restricted templates. These approaches give traceable and repeatable results when requirements are written in a controlled form (L2, L27) or modelled in BPMN (L24), but such input is rare in practice, and rewriting requirements by hand removes most of the time saving. Reviews (L4, L6) name unstructured and low-quality requirements as the main obstacle.

**LLM-based generation (L5, L7–L13, L25, L26).** Recent studies show that LLMs can draft useful test cases from free-form requirements: most cases are judged valid or helpful (L9, L10), expert ratings reach 4.75–4.8 of 5 with strong cloud models (L25, L26), and retrieval with few-shot examples improves results (L7, L25). The same studies show the limits: correctness is rated lower than fluency (L7), a share of cases is redundant or not applicable (L9, L22), results depend strongly on the dataset (L11), and vague requirements reduce effectiveness (L12). Human review therefore remains necessary.

**Local and small models (L13, L19–L22, L25).** Most studies rely on proprietary cloud models. Evidence for local open-weight models is growing but mixed: fine-tuned 8B models approached a strong cloud model (L13), and small tuned models matched zero-shot cloud models in classification (L20); however, a 7B model scored clearly lower than GPT-4o in SRS-based generation (L25), and a fine-tuned Llama-2-7B produced many near-duplicate tests (L22). This is why we compare several model sizes (8B–30B class) and add a verifier.

**Evaluation practice (L6, L11, L19, L25).** Studies use different methods: expert ratings, BLEU/ROUGE against reference cases, semantic similarity, model-based coverage and mutation scores (L8, L12). Similarity metrics can disagree with expert judgement (L19), and surveys note the lack of standard benchmarks (L6, L14). We therefore use coverage, acceptance and hallucination rates as primary metrics and BLEU/ROUGE-L only as secondary ones (Section 9).

**Risks (L17, L18, S3).** Hallucination and indirect prompt injection through uploaded documents are documented risks; no complete defence exists, so both are measured, not assumed away. No studies on Russian- or Kazakh-language requirements were found so far; this is recorded as an open point of the search.

## 3.4 Limitations the Project Takes into Account

*Table 3.3 – Known limitations and how the project addresses them*

| Known limitation (source) | How the project addresses it | Where |
|---|---|---|
| Correctness lower than coherence (L7, L9) | Mandatory human review; acceptance rate as a primary metric | FR-08, Section 9 |
| Redundant or not applicable cases (L9, L22) | Verifier with duplicate detection; duplicate rate measured | FR-07, Section 9 |
| Vague requirements reduce effectiveness (L6, L12, L27) | Quality gate flags ambiguity before generation | FR-04 |
| Naive refinement loops can hurt (L12) | Retries limited to schema repair (≤ 2); any loop evaluated in an ablation | NFR-AIQ-01, Section 9 |
| No standard benchmark (L6, L14) | Own dataset with gold cases, inter-rater agreement, published scripts | Section 9.3 |
| Similarity metrics disagree with experts (L19, L25) | BLEU/ROUGE-L only secondary; expert acceptance is primary | Section 9.5 |
| Weak traceability and hallucination control (L14) | Every case cites existing requirement IDs; hallucination rate measured | FR-06, NFR-AIQ-03 |
| Prompt injection via uploaded content (L17, S3) | Document text treated as data; no tools for the model; schema-validated output; red-team set | NFR-SEC-04 |
| Evidence mostly from cloud models (L7–L11, L25, L26) | Benchmark of local models; a cloud model only as a reference on public data | Section 9.4 |

## 3.5 Research Gap

In the reviewed literature and in the systems compared in Section 4 we did not find a solution that combines all of the following: (1) schema-validated, structured test cases, (2) fully on-premise execution with an open-weight model, (3) a requirement quality check based on ISO/IEC/IEEE 29148 before generation, and (4) requirement-level traceability with measured hallucination and duplicate rates. Single elements exist (RAG and few-shot in L7 and L25, schema-aware prompting in L26, fine-tuned local models in L13); the contribution of the project is their combination and its measured evaluation on English and Russian requirements.

## 3.6 References

[L1] V. Garousi, S. Bauer, M. Felderer, "NLP-assisted software testing: A systematic mapping of the literature," Information and Software Technology, vol. 126, 106321, 2020. doi:10.1016/j.infsof.2020.106321

[L2] C. Wang, F. Pastore, A. Göknil, L. Briand, "Automatic Generation of Acceptance Test Cases From Use Case Specifications: An NLP-Based Approach," IEEE Transactions on Software Engineering, vol. 48, no. 2, pp. 585–616, 2022 (online 2020). doi:10.1109/TSE.2020.2998503

[L3] L. Zhao, W. Alhoshan, A. Ferrari, K. J. Letsholo, M. A. Ajagbe, E.-V. Chioasca, R. T. Batista-Navarro, "Natural Language Processing for Requirements Engineering: A Systematic Mapping Study," ACM Computing Surveys, vol. 54, no. 3, art. 55, 2021. doi:10.1145/3444689

[L4] A. Mustafa, W. M. N. Wan-Kadir, N. Ibrahim, M. A. Shah, M. Younas, A. Khan, M. Zareei, F. Alanazi, "Automated test case generation from requirements: A systematic literature review," Computers, Materials & Continua, vol. 67, no. 2, pp. 1819–1833, 2021. doi:10.32604/cmc.2021.014391

[L5] J. Wang, Y. Huang, C. Chen, Z. Liu, S. Wang, Q. Wang, "Software Testing With Large Language Models: Survey, Landscape, and Vision," IEEE Transactions on Software Engineering, vol. 50, no. 4, pp. 911–936, 2024. doi:10.1109/TSE.2024.3368208

[L6] Z. Yang, R. Huang, C. Cui, N. Niu, D. Towey, "Requirements-Based Test Generation: A Comprehensive Survey," arXiv:2505.02015, 2025.

[L7] C. Arora, T. Herda, V. Homm, "Generating Test Scenarios from NL Requirements using Retrieval-Augmented LLMs: An Industrial Study," arXiv:2404.12772, 2024.

[L8] B. R. Korraprolu, P. Pinninti, R. Reddy, "Test Case Generation for Requirements in Natural Language — An LLM Comparison Study," in Proc. Innovations in Software Engineering Conference (ISEC 2025), 2025.

[L9] S. Bhatia, T. Gandhi, D. Kumar, P. Jalote, "System Test Case Design from Requirements Specifications: Insights and Challenges of Using ChatGPT," arXiv:2412.03693, 2024.

[L10] M. Ferreira, L. Viegas, J. P. Faria, B. Lima, "Acceptance Test Generation with Large Language Models: An Industrial Case Study," in Proc. IEEE/ACM International Conference on Automation of Software Test (AST 2025), 2025. doi:10.1109/AST66626.2025.00007 (preprint arXiv:2504.07244)

[L11] S. Masuda, S. Kouzawa, K. Sezai, H. Suhara, Y. Hiruta, K. Kudou, "Generating High-Level Test Cases from Requirements using LLM: An Industry Study," arXiv:2510.03641, 2025.

[L12] L. Kogler, S. Hangler, M. Ehrhart, B. Dornauer, R. Wuersching, P. Schrammel, "RESTestBench: A Benchmark for Evaluating the Effectiveness of LLM-Generated REST API Test Cases from NL Requirements," arXiv:2604.25862, 2026.

[L13] M. Moradi, K. Yan, D. Colwell, R. Asgari, "An empirical study of LoRA-based fine-tuning of large language models for automated test case generation," arXiv:2604.06946, 2026.

[L14] O. Folorunsho, H. Reza, "AI-Driven Test Case Generation from Natural Language Requirements: A Survey of Techniques and Research Gaps," arXiv:2606.06563, 2026.

[L15] P. Lewis et al., "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks," in Advances in Neural Information Processing Systems 33 (NeurIPS 2020), pp. 9459–9474, 2020.

[L16] W. Kwon et al., "Efficient Memory Management for Large Language Model Serving with PagedAttention," in Proc. 29th ACM Symposium on Operating Systems Principles (SOSP '23), pp. 611–626, 2023. doi:10.1145/3600006.3613165

[L17] K. Greshake, S. Abdelnabi, S. Mishra, C. Endres, T. Holz, M. Fritz, "Not What You've Signed Up For: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection," in Proc. 16th ACM Workshop on Artificial Intelligence and Security (AISec '23), pp. 79–90, 2023. doi:10.1145/3605764.3623985

[L18] Z. Ji et al., "Survey of Hallucination in Natural Language Generation," ACM Computing Surveys, vol. 55, no. 12, pp. 1–38, 2023. doi:10.1145/3571730

[L19] A. Tugambayeva, A. Sakhipov, "AI-based question generation for aviation training: Comparing retrieval-augmented generation and fine-tuned models," Scientific Journal of Astana IT University, vol. 25, 2026. doi:10.37943/25VYNZ9998

[L20] D. Kapizov, P. Kumar, "Fine-tuning small language models for mental health text classification: A parameter-efficient approach outperforming zero-shot large language models," Scientific Journal of Astana IT University, 2026. doi:10.37943/XSAJ1029

[L21] A. Mansurova, A. Nugumanova, Zh. Makhambetova, "Development of a question answering chatbot for blockchain domain," Scientific Journal of Astana IT University, vol. 15, 2023. doi:10.37943/15XNDZ6667

[L22] S. Rehan, B. Al-Bander, A. Al-Said Ahmad, "Harnessing Large Language Models for Automated Software Testing: A Leap Towards Scalable Test Case Generation," Electronics, vol. 14, no. 7, 1463, 2025. doi:10.3390/electronics14071463

[L23] I. Al-Azzoni, S. Iqbal, T. Al Ashkar, Z. Erum, "Integrating Model-Driven Engineering and Large Language Models for Test Scenario Generation for Smart Contracts," Information, vol. 17, no. 1, art. 1, 2026 (online 19 Dec 2025). doi:10.3390/info17010001

[L24] D. Mateus, D. S. da Silveira, J. Araujo, "Pattern-Based Automation of User Stories and Gherkin Scenarios from BPMN Models for Agile Requirement," Applied Sciences, vol. 15, no. 17, 9434, 2025. doi:10.3390/app15179434

[L25] M. Boukhlif, N. Kharmoum, M. Hanine, "Leveraging Retrieval-augmented LLMs for Automated Test Case Generation from Software Requirements Specification," International Journal of Intelligent Engineering and Systems, vol. 19, no. 1, 2026. doi:10.22266/ijies2026.0131.04

[L26] A. F. Almeyda Alania, A. Barrientos Padilla, R. G. Siancas Garay, "Engineering Prompt-Orchestrated LLM Workflows for Automated Test Case Generation in Agile Environments," International Journal of Advanced Computer Science and Applications, vol. 16, no. 12, 2025. doi:10.14569/IJACSA.2025.0161272

[L27] A. Intana, K. Tantayakul, K. Laosen, S. Charoenreh, "An Approach of Test Case Generation with Software Requirement Ontology," International Journal of Advanced Computer Science and Applications, vol. 14, no. 8, 2023. doi:10.14569/IJACSA.2023.01408109

[S1] ISO/IEC/IEEE 29148:2018, Systems and software engineering — Life cycle processes — Requirements engineering.

[S2] ISO/IEC/IEEE 29119-4:2021, Software and systems engineering — Software testing — Part 4: Test techniques.

[S3] OWASP Foundation, OWASP Top 10 for LLM Applications, 2025. https://genai.owasp.org/
