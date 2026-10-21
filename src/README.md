# Source code

Code starts after pre-defense-1. Planned layout (see docs/07-architecture.md):

| Folder | Content | Owner |
|---|---|---|
| `backend/` | FastAPI application: auth, documents & parser, requirements, jobs, review, export, admin; Alembic migrations | Sultan (S2), Kaisar (review/export API) |
| `frontend/` | Next.js application: upload, generation, review, traceability, export screens | Kaisar (S3) |
| `ai/` | Worker: AI pipeline, `LLMProvider` adapters (Ollama, vLLM, fake), prompts (versioned), verifier | Nuraly (S1) |

Every module is developed test-first where practical; see docs/09 for the gates.
