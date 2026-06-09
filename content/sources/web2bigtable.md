---
type: source
arxiv_id: "2604.27221"
title: "Web2BigTable: A Bi-Level Multi-Agent LLM System for Internet-Scale Information Search and Extraction"
authors: ["Unknown"]
date: 2026-04-23
org: "Unknown"
tags: [agents, multi-agent-systems, web-search, information-extraction, 2026]
upvotes: 6
---

# Web2BigTable: Bi-Level Multi-Agent LLM System for Internet-Scale Search

> A multi-agent framework for web-to-table search that supports both breadth-oriented (wide) and depth-oriented (deep) search regimes through bi-level architecture with closed-loop run-verify-reflect adaptation.

## Key Contributions

- **Bi-level architecture**: Upper-level orchestrator decomposes queries into subtasks; lower-level worker agents execute in parallel
- **Closed-loop run-verify-reflect process**: Jointly refines task decomposition and worker execution through persistent, editable external memory — LLMs remain frozen, adaptation happens via memory updates
- **Asynchronous coordination**: Workers share progress through a shared workspace (Workboard), reducing redundant exploration, reconciling conflicting evidence, and responding to coverage gaps
- **State-of-the-art results**: 7.5× better Avg@4 Success Rate (38.50 vs 5.10) on WideSearch; strong generalization to XBench-DeepSearch (73.0 accuracy)

## Method

Addresses limitations of monolithic agents and fixed-plan hierarchical frameworks:
- **Wide search** (e.g., "list every Taylor Swift concert 2010–2025") requires broad coverage and verification at scale
- **Deep search** (e.g., "member of Korean girl group with brother 12 years younger") requires chaining indirect clues

Two skill banks evolve over time:
- **Orchestrator Skills (𝒮ₒ)**: Task decomposition strategies
- **Worker Skills (𝒮ᵥ)**: Retrieval, evidence verification, intermediate synthesis skills

## Results

| Metric | Web2BigTable | Second Best | Gap |
|---|---|---|---|
| Avg@4 Success Rate | 38.50 | 5.10 | **7.5×** |
| Row F1 | 63.53 | 38.50 | **+25.03** |
| Item F1 | 80.12 | 65.70 | **+14.42** |
| XBench-DeepSearch | 73.0 | — | Strong generalization |

## Connections
- Builds on: [[sources/eywa]], [[sources/agentic-rl-reasoning]], [[sources/multi-turn-agent-rl]]
- Related concepts: [[concepts/agents]], [[concepts/multi-agent-systems]], [[concepts/rag]]
- Related papers: [[sources/react]], [[sources/codeact]], [[sources/claw-eval-live]]
- Cited by / Influenced: Multi-agent web search, agentic information systems

## Citation
> "Web2BigTable: A Bi-Level Multi-Agent LLM System for Internet-Scale Information Search and Extraction," arXiv:2604.27221, 2026.
