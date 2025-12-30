# Financial Agent Benchmark Project (RAG + LLM Comparison)

## Overview

This project implements and evaluates **agent-based financial question answering systems** using
Retrieval-Augmented Generation (RAG), external financial tools, and Large Language Models (LLMs).

The goal is to compare **answer quality, reasoning reliability, hallucination resistance, and cost efficiency**
across different LLM backends under identical benchmark conditions.

The project focuses on **Eurobond analysis, tax rules, policy interpretation, and financial calculations**.

---

## Implemented Approaches

The project evaluates **three main approaches**:

### 1. Groq-Based Agent (LLaMA-3)

- Uses Groq API with LLaMA-3 family models
- Agent-style reasoning loop
- Tool usage (calculator, market data, RAG)
- Optimized for **low latency and low cost**

### 2. GPT-4o-mini Agent

- Uses OpenAI GPT-4o-mini
- Strong document grounding
- Conservative, compliance-oriented reasoning
- Higher cost but stronger hallucination resistance

### 3. Gemini + Chroma (Soft-Agent)

- Gemini Flash / Pro models
- No strict ReAct parsing (safe generation)
- Persistent ChromaDB as document store
- Focus on robustness under rate limits

---

## System Architecture

Documents (PDF / TXT)
↓
ChromaDB (Persistent Vector Store)
↓
Semantic Retrieval (RAG)
↓
LLM Prompt Injection
↓
LLM Reasoning
↓
Deterministic Tools
↓
Final Answer


---


## Knowledge Base

Indexed documents include:
- Eurobond bulletins
- HSBC Eurobond policy and risk documentation
- Turkish tax regulations (Eurobond income)
- Fund prospectuses (AKE fund)
- Supplementary rate and reference files

The knowledge base is stored in **persistent ChromaDB**, allowing reuse across sessions.

---

## Benchmark Design

The benchmark is **scenario-based** and includes over **40 financial questions**, grouped into:

- Comparison & Ranking
- Logic & Math
- Multi-Hop Reasoning
- Fallback Behavior
- Hallucination Resistance
- Temporal Reasoning
- Policy & Risk Interpretation
- Complex Financial Scenarios

Each scenario is logged and exported as **JSON** for offline analysis.

---

## Evaluation Criteria

Each agent is evaluated on:

- Answer correctness
- Use of retrieved context
- Mathematical accuracy
- Handling of missing data
- Hallucination avoidance
- Consistency across runs
- Token-based cost

---

## Cost Comparison (Approximate)

| Model            | Cost per 1K Tokens | Notes |
|------------------|-------------------|------|
| Groq (LLaMA-3)   | ~$0.0001          | Extremely low cost |
| GPT-4o-mini      | ~$0.0011          | Higher reliability |
| Gemini Flash     | Low–Medium        | Rate-limited |

### Estimated Full Benchmark Cost (~40 scenarios)

| Model        | Total Cost |
|-------------|-----------|
| Groq        | ~$0.01–0.02 |
| GPT-4o-mini | ~$0.04–0.05 |
| Gemini      | Depends on quota |

---

## Key Insight

In financial systems, **refusing to answer due to missing data is often correct behavior**.

An agent that answers fewer questions but avoids hallucination is safer and more suitable
for **regulated financial environments**.

---

## Final Recommendation

- Use **Groq-based agents** for:
  - Rapid experimentation
  - Cost-sensitive analysis
  - Large-scale batch reasoning

- Use **GPT-4o-mini agents** for:
  - Client-facing systems
  - Compliance-sensitive applications
  - High-stakes financial decisions

A **hybrid architecture** combining both is recommended.

---

## Outputs

- `groq_outputs_clean.json` – Cleaned Groq benchmark outputs
- `benchmark_results_gpt4o_mini.json` – GPT-4o-mini benchmark results
- Persistent ChromaDB under `/content/drive/.../chroma_db_persistent`

---

## Future Work

- Ensemble agent voting
- Confidence scoring
- Rule-based post-validation
- Financial-domain fine-tuning
- Automated regression benchmarks

---

## Author Notes

This project is designed as a **research-grade evaluation framework**
and can be extended to other financial instruments or regulatory domains.

