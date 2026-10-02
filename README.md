# Cost-Aware RAG with Semantic Caching and Intelligent LLM Routing

A cost-aware Retrieval-Augmented Generation (RAG) system that combines semantic caching and intelligent LLM routing to reduce LLM inference cost while maintaining retrieval quality and semantic answer consistency.

## Overview

Traditional RAG systems can send every user query to a large language model, even when a similar query has already been answered or when the query does not require a larger model.
This project investigates two cost-optimization techniques:

- **Semantic caching** — reuse answers for semantically similar queries.
- **Intelligent LLM routing** — select between a smaller and larger language model based on query characteristics.
The system uses the **SciFact** dataset for scientific document retrieval and **Groq-hosted GPT-OSS models** for answer generation.

## Key Results

The final system was evaluated on a 20-request experimental workload.
| Metric | Result |
|---|---:|
| Retrieval Recall@1 | 48.23% |
| Retrieval Recall@5 | 73.79% |
| Retrieval Recall@10 | 78.33% |
| Retrieval MRR | 60.47% |
| Semantic Cache Hit Rate | 55.00% |
| Total Requests | 20 |
| LLM Calls | 9 |
| GPT-OSS-20B Calls | 4 |
| GPT-OSS-120B Calls | 5 |
| Average Semantic Answer Similarity | 0.8671 |
| Always GPT-OSS-120B Cost | $0.008408 |
| Final System Cost | $0.003025 |
| Estimated Cost Reduction | 64.03% |

## Ablation Study

| Strategy | Estimated Cost | Cost Reduction vs. 120B |
|---|---:|---:|
| Always GPT-OSS-20B | $0.004110 | 51.12% |
| Always GPT-OSS-120B | $0.008408 | 0% |
| Semantic Cache Only | $0.004204 | 50.00% |
| Router Only | $0.006831 | 18.75% |
| Semantic Cache + Router | $0.003025 | 64.03% |

> Cost results represent the evaluated 20-request workload and are experimental estimates based on measured token usage and applicable model pricing.

## Technology Stack
- Python
- Google Colab
- Pandas
- NumPy
- FAISS
- Sentence Transformers
- Groq API
- GPT-OSS-20B
- GPT-OSS-120B
- Matplotlib
- SciFact / BEIR
