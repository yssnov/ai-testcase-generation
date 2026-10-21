# Tests

| Folder (planned) | Level | Tools |
|---|---|---|
| `unit/` | Domain and service logic with a fake LLM | pytest, Vitest |
| `contract/` | Same suite against each LLM provider and exporter | pytest |
| `integration/` | API + PostgreSQL (testcontainers), worker crash/retry, IDOR | pytest |
| `e2e/` | Scenarios 1–4 in the browser | Playwright |
| `load/` | PERF-1…PERF-3 | k6 |
| `security/` | Red-team prompt-injection documents, negative upload files | pytest |

Plan and targets: docs/09-verification-evaluation-plan.md.
