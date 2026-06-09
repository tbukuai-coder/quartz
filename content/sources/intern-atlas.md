---
type: source
arxiv_id: "2604.28158"
title: "Intern-Atlas: A Methodological Evolution Graph as Research Infrastructure for AI Scientists"
authors: ["Shanghai AI Lab / Multiple Institutions"]
date: 2026-04-25
org: "Shanghai AI Laboratory"
tags: [agents, research-infrastructure, knowledge-graphs, scientific-discovery, 2026]
upvotes: 39
---

# Intern-Atlas: Methodological Evolution Graph for AI Scientists

> A methodological evolution graph that processes papers from top-tier venues, extracts method entities with alias resolution, classifies citation edges into semantic types, and grounds each edge in verbatim quotes — providing a queryable causal topology for automated scientific discovery.

## Key Contributions

- **Methodological evolution graph**: Makes method evolution (e.g., Transformer → BERT/GPT/ViT) explicit as a typed graph with causal edge labels
- **Self-Guided Temporal Monte Carlo Tree Search (SGT-MCTS)**: Balances exploitation of high-confidence paths with exploration of under-visited branches while enforcing temporal coherence
- **Agent-readable infrastructure**: Unlike citation-based tools (Google Scholar, Semantic Scholar), Atlas provides direct queries for method lineage, bottleneck evidence, idea evaluation, and idea generation
- **Three-dimensional evaluation**: Graph quality vs. expert chains, idea evaluation with graph-grounded scoring, idea generation with/without evolutionary context

## Key Insights

- Historical pattern: structured knowledge infrastructure precedes its full utilization (PDB → AlphaFold, ImageNet → CNNs, now methodology graphs → AI research agents)
- AI agents cannot reconstruct method evolution topologies from unstructured text; their parametric memory is lossy and autoregressive inference is fixed-depth forward computation
- Methodological progress forms a directed acyclic graph; greedy traversal discards alternative trajectories
- Graph-grounded scoring signals exhibit monotonic alignment with human tiers

## Connections
- Builds on: [[sources/eywa]], [[sources/agent-native-research-artifact]], [[concepts/agents]]
- Related concepts: [[concepts/llm-evaluation]], [[concepts/synthetic-data]]
- Related papers: [[sources/learning-while-deploying]], [[sources/web2bigtable]]

## Citation
> "Intern-Atlas: A Methodological Evolution Graph as Research Infrastructure for AI Scientists," arXiv:2604.28158, 2026.
