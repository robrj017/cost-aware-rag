# Cost-Aware RAG with Semantic Caching and Intelligent LLM Routing

A cost-aware Retrieval-Augmented Generation (RAG) system that combines **semantic caching** and **intelligent LLM routing** to reduce LLM inference cost while maintaining retrieval quality and semantic answer consistency.

---

## Problem Statement

RAG systems can become expensive when every query is sent to a large language model, even when:

- a similar question has already been answered
- the query does not require the largest model
- repeated requests could reuse an existing response

This project investigates whether **semantic caching** and **cost-aware model routing** can reduce LLM inference cost while preserving retrieval quality and semantic consistency.

---

## Solution Overview

The system combines two optimization mechanisms.

### 1. Semantic Caching

Before calling an LLM, the system checks whether a semantically similar query has already been answered.

If a sufficiently similar cached query exists, the previous answer can be reused without making another LLM call.

### 2. Intelligent LLM Routing

For cache misses, the system selects between two models:

- **GPT-OSS-20B** — lower-cost model
- **GPT-OSS-120B** — larger model for more complex queries

This creates a cost-aware RAG pipeline instead of sending every request to the largest model.

---

## System Workflow

```text
User Query
    │
    ▼
Query Embedding
    │
    ▼
Semantic Cache
    │
    ├──────── Cache Hit ────────► Cached Answer
    │
    ▼
Cache Miss
    │
    ▼
FAISS Retrieval
    │
    ▼
Cost-Aware Router
    │
    ├────────► GPT-OSS-20B
    │
    └────────► GPT-OSS-120B
                    │
                    ▼
             Grounded Answer
