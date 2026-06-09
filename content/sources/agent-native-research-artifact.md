---
type: source
arxiv_id: "2604.24658"
title: "The Last Human-Written Paper: Agent-Native Research Artifacts"
authors: ["Orchestra Research"]
date: 2026-04-14
org: "Orchestra Research"
tags: [agents, research-infrastructure, scientific-publishing, reproducibility, 2026]
upvotes: 13
---

# Agent-Native Research Artifacts (Ara)

> A protocol that recasts the primary research object from narrative PDF to agent-executable knowledge package, addressing the "Storytelling Tax" and "Engineering Tax" that current publication formats impose on AI research agents.

## Key Contributions

- **Quantified compilation costs**: Analysis of 24,008 agent runs shows failed runs account for 90.2% of total dollar cost; median failed-to-success token ratio is 113× when agents lack prior failure records
- **Engineering Tax quantification**: Only 45.4% of PaperBench reproduction requirements are fully specified in papers+code; missing hyperparameters alone account for 26.2% of all gaps
- **Agent-Native Research Artifact (Ara) protocol**: Four-layer structure — structured scientific logic, executable code with full operational specs, exploration graph preserving branching research process, grounded evidence binding claims to raw outputs
- **Rationale**: AI agents benefit from exhaustive detail while humans need concise narrative; current PDFs serve neither audience optimally

## Key Insights

- Research proceeds as a branching tree with dead ends, but publication compiles it into a linear narrative discarding all failure knowledge
- The emergence of capable AI agents creates a new knowledge consumer that requires structured, lossless, executable artifacts
- Historical pattern: structured knowledge infrastructure becomes essential when automated systems emerge that cannot operate over unstructured data (PDB → AlphaFold, ImageNet → CNNs)
- Current efforts (FAIR principles, RO-Crate, AGENTS.md) address fragments but don't jointly structure logic, code, and exploration history

## The Ara Protocol

Four interlocking layers:
1. **Structured scientific logic**: Queryable claims and dependency graphs
2. **Executable code**: Full operational specifications (not just reviewer-sufficient descriptions)
3. **Exploration graph**: Preserves failed experiments, rejected hypotheses, design pivots
4. **Grounded evidence**: Binds every claim to raw empirical outputs

## Connections
- Builds on: [[sources/intern-atlas]], [[sources/agentic-rl-reasoning]], [[concepts/agents]]
- Related concepts: [[concepts/llm-evaluation]], [[concepts/synthetic-data]]
- Related comparisons: [[comparisons/open-science-vs-open-weight]]
- Cited by / Influenced: Future of scientific publishing and AI-assisted research

## Citation
> "The Last Human-Written Paper: Agent-Native Research Artifacts," arXiv:2604.24658, 2026.
