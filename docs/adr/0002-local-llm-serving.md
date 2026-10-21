# ADR-0002: Ollama for development, vLLM for production, behind one provider interface

- **Status:** Proposed
- **Date:** 2026-10-__
- **Owner:** Nuraly Abat

## Context
The system must use a locally hosted model (constraint C-01). Developers need a quick local setup; production must serve ~10 parallel generation jobs at peak (NFR-PERF-02).

## Options
Ollama; vLLM; llama.cpp server (comparison in 05, D1).

## Decision
Code against an `LLMProvider` interface that calls an OpenAI-compatible endpoint. Use Ollama on developer machines and vLLM on the GPU server; keep llama.cpp as a CPU fallback for demos.

## Consequences
+ Model and runtime are configuration, not code (`LLM_BASE_URL`, `LLM_MODEL`).
+ We can measure and report the runtime difference (09).
− Structured-output parameters differ slightly between runtimes; contract tests run against each provider.
− vLLM needs Linux + NVIDIA GPU (dependency D-01 in 10).
