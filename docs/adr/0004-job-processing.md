# ADR-0004: Postgres-backed job queue with Server-Sent Events for progress

- **Status:** Proposed
- **Date:** 2026-10-__
- **Owners:** Sultan Muratbek, Nuraly Abat

## Context
Generating test cases for a document takes from seconds to minutes. HTTP requests must not wait that long; jobs must survive worker crashes; the UI must show progress.

## Options
Postgres-backed queue + SSE; Redis/Celery + WebSocket; synchronous REST (comparison in 05, D4).

## Decision
The API creates a job row and returns `202 Accepted` with the job ID. A worker claims jobs with `SELECT … FOR UPDATE SKIP LOCKED`, writes results in one transaction, and publishes progress that the UI reads through an SSE endpoint.

## Consequences
+ No extra infrastructure; a crashed worker releases its lock and the job is retried.
+ Easy to test (integration test kills the worker mid-job).
− SSE is one-way; user actions use normal REST calls.
− If queue throughput becomes a bottleneck, revisit with Redis (measure first).
