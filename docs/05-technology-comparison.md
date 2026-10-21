# 5. Technology Comparison and Justification

Six technical decisions were compared, each with three alternatives. Every criterion refers to a requirement from Section 6. Scale: ++ strong fit, + fit, 0 neutral, − weak fit. The scores are the team's judgement supported by the cited sources; where a number matters (throughput, latency), it will be measured in the benchmark (Section 9), not taken from vendor claims. Each accepted decision is recorded as an Architecture Decision Record (ADR) in the repository.

## 5.1 D1. Local LLM Serving Runtime (Owner: Nuraly Abat)

*Table 5.1 – LLM serving runtime*

| Criterion (requirement) | Ollama | vLLM | llama.cpp server |
|---|---|---|---|
| OpenAI-compatible API, backend runtime-agnostic (NFR-MAINT-02) | ++ | ++ | ++ |
| Concurrent jobs at peak load, ~10 parallel (NFR-PERF-02) | − (limited batching) | ++ (continuous batching, PagedAttention [L16]) | 0 |
| Ease of local development on laptops | ++ | − (Linux + NVIDIA GPU) | + |
| Structured JSON-schema output (FR-05, NFR-AIQ-01) | + | + | + (grammars) |
| Runs quantised models on a 12–24 GB consumer GPU (budget C-02) | ++ | + | ++ (also CPU) |
| Decision | Development and experiments | Production and load tests | Fallback for a CPU-only demo |

**Decision.** vLLM is selected for production because PagedAttention and continuous batching maximise throughput on limited GPU resources [L16]. Ollama is kept for local development and rapid experiments. A single LLMProvider interface (module 8) allows switching runtimes by configuration; Ollama vs vLLM throughput and latency are reported in the experiment.

## 5.2 D2. Backend Platform (Owner: Sultan Muratbek)

*Table 5.2 – Backend platform*

| Criterion (requirement) | Python + FastAPI | Python + Django REST Framework | Java + Spring Boot |
|---|---|---|---|
| Ecosystem for LLM, embeddings, document parsing (FR-02, FR-05) | ++ | ++ | 0 |
| Async I/O for streaming progress and long LLM calls (FR-05, NFR-PERF-01) | ++ (native async) | + | + |
| Typed API contract and automatic OpenAPI docs (NFR-MAINT-02) | ++ (Pydantic) | + (extra packages) | + |
| Built-in admin, auth, ORM | 0 (assembled from libraries) | ++ | ++ |
| Decision | Chosen | Alternative | Rejected: weaker AI ecosystem for our tasks |

**Decision.** Python + FastAPI: asynchronous performance, Pydantic models that map directly to the JSON schemas of test cases, and automatic OpenAPI documentation that serves as the contract between frontend and backend. The system is built as a modular monolith (one deployable backend with clear module boundaries) to keep operations simple.

## 5.3 D3. Data Storage and Vector Search (Owner: Sultan Muratbek)

*Table 5.3 – Data storage*

| Criterion (requirement) | PostgreSQL + pgvector | PostgreSQL + separate vector DB (Qdrant) | SQLite + FAISS |
|---|---|---|---|
| ACID transactions for jobs, cases and links (NFR-REL-02) | ++ | + (two stores, no shared transaction) | + (single user) |
| Vector similarity for duplicates and RAG (FR-07, FR-12) | + (HNSW index) | ++ | + |
| Constraints, views, triggers for traceability and audit (FR-09, NFR-SEC-05) | ++ | ++ (relational part) | 0 |
| Number of services to run and back up (C-02, NFR-OPS-01) | ++ (one) | − (two) | ++ |
| Multi-user web load (NFR-PERF-02) | ++ | ++ | − |
| Decision | Chosen | Alternative if vector volume grows | Rejected |

**Decision.** PostgreSQL with pgvector provides ACID guarantees, relational integrity for requirement–test-case links and vector search in one engine, without the operational overhead of a separate vector database.

## 5.4 D4. Component Interaction for Long-Running Generation (Owners: Sultan Muratbek, Nuraly Abat)

*Table 5.4 – Interaction method*

| Criterion (requirement) | REST + Postgres job queue + SSE | REST + Redis/Celery + WebSocket | Synchronous REST call |
|---|---|---|---|
| No lost jobs if a worker crashes (NFR-REL-01) | ++ (row lock, retry) | + (depends on broker settings) | − |
| Live progress in the UI (FR-05) | + (SSE, one-way) | ++ (two-way) | − |
| Extra infrastructure (C-02) | ++ (none) | − (Redis + Celery) | ++ |
| Request time-outs under load (NFR-PERF-01) | ++ | ++ | − (requests last minutes) |
| Decision | Chosen | Alternative if throughput requires | Rejected |

**Decision.** A PostgreSQL-backed job queue (SELECT … FOR UPDATE SKIP LOCKED for safe concurrent dequeuing) combined with Server-Sent Events for real-time progress. No additional broker is needed, and a crashed job is retried automatically.

## 5.5 D5. Frontend Framework (Owner: Kaisar Yessenov)

*Table 5.5 – Frontend framework*

| Criterion (requirement) | Next.js (React, TypeScript) | React SPA with Vite | Vue 3 / Nuxt |
|---|---|---|---|
| Component ecosystem for data-heavy review tables and diffs (FR-08, FR-09) | ++ | ++ | + |
| UI languages EN/RU/KK (NFR-LANG-02) | + (next-intl) | + (i18next) | + (vue-i18n) |
| Accessibility and testing tools (NFR-USAB-02) | ++ | ++ | + |
| Fast initial load (server-side rendering) | ++ | 0 | ++ (Nuxt) |
| Deployment in Docker behind Caddy (NFR-OPS-01) | + (Node server) | ++ (static files) | + |
| Decision | Chosen | Strong alternative | Alternative |

**Decision.** Next.js (React + TypeScript): server-side rendering for fast initial loads, a rich ecosystem for complex tables and diff views needed in the review workflow, and internationalisation through next-intl.

## 5.6 D6. Model Family (Owner: Nuraly Abat)

*Table 5.6 – Candidate open-weight models*

| Criterion | Qwen3 (8B / 14B / 30B-A3B) | Gemma (latest open release) | Mistral (7B / Small) |
|---|---|---|---|
| Quality on our dataset (NFR-AIQ-01…03) | To be measured | To be measured | To be measured |
| Russian-language quality (NFR-LANG-01) | To be measured | To be measured | To be measured |
| Latency and VRAM on the target GPU (NFR-PERF-03) | To be measured | To be measured | To be measured |
| Licence (prefer Apache-2.0 / MIT) | Recorded per model | Recorded per model | Recorded per model |

**Decision.** The model is chosen by measurement, not now: after benchmark round 1 (December 2026). Embedding model candidate: BGE-M3 (multilingual). Section 3 shows that model size matters for this task (L25), so 3–4 models of different sizes are compared.

Detailed decision records: [ADR-0001](adr/0001-architecture-style.md), [ADR-0002](adr/0002-local-llm-serving.md), [ADR-0003](adr/0003-data-storage.md), [ADR-0004](adr/0004-job-processing.md).
