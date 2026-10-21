# ADR-0003: PostgreSQL with pgvector as the single data store

- **Status:** Proposed
- **Date:** 2026-10-__
- **Owner:** Sultan Muratbek

## Context
We store users, projects, documents, requirements (with embeddings), generation jobs, test cases, requirement–test links and an audit log. We need transactions, constraints, views (traceability, coverage), triggers (audit, timestamps) and similarity search (duplicates, RAG).

## Options
PostgreSQL + pgvector; PostgreSQL + separate vector database; SQLite + FAISS (comparison in 05, D3).

## Decision
PostgreSQL with the pgvector extension; schema changes only through Alembic migrations.

## Consequences
+ One service to run, monitor and back up; job results, cases and links written in one ACID transaction.
+ Views and triggers give traceability and audit without application code.
− Vector search performance must be checked on our data volume (EXPLAIN ANALYZE in Chapter 3).
