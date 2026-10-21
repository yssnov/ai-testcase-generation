# ADR-0001: Modular monolith with FastAPI backend

- **Status:** Proposed (accept after team review in PR)
- **Date:** 2026-10-__
- **Owner:** Sultan Muratbek

## Context
Three developers, about seven months, infrastructure budget up to USD 50, target ~1,000 users/day (≈2,000 generation jobs/day). The heavy work is LLM inference, which runs in a separate LLM server anyway.

## Options
1. Modular monolith: one backend (FastAPI) with modules auth, documents, requirements, generation, review, export, evaluation; one worker process; one database.
2. Microservices: separate services per module with a message broker.
3. Serverless functions.

## Decision
Option 1. Modules communicate through interfaces (Python protocols), so a module can be extracted later. The LLM server stays a separate process behind an OpenAI-compatible API.

## Consequences
+ One image, one database, simple CI/CD and debugging; fits budget and team size.
+ Load target is far below the scale where microservices pay off.
− Modules share a deployment; discipline is needed to keep boundaries (enforced by code review and package structure).
Version pinned: Python ____, FastAPI ____ (fill when accepted).
