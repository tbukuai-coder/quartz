---
type: source
arxiv_id: "2605.05242"
title: "Beyond Semantic Similarity: Rethinking Retrieval for Agentic Search via Direct Corpus Interaction"
authors: ["Zhuofeng Li", "Haoxiang Zhang", "Cong Wei", "Pan Lu", "Ping Nie", "Yi Lu", "Yuyang Bai", "Shangbin Feng", "Hangxiao Zhu", "Ming Zhong"]
date: 2026-05
tags: [retrieval, agents, corpus-interaction, lexical-retrieval, semantic-retrieval, rag, agentic-search]
upvotes: 2
---

# Beyond Semantic Similarity: Rethinking Retrieval for Agentic Search via Direct Corpus Interaction

> Direct corpus interaction (DCI) enables more effective agentic search by allowing agents to query raw text directly, outperforming traditional similarity-based retrieval methods in complex multi-hop reasoning and sparse clue conjunction tasks.

## Key Contributions
- Argues that conventional retrieval systems (lexical and semantic) compress corpus access into a single top-k step, which is a bottleneck for agentic search
- Identifies tasks where fixed similarity interfaces fail: exact lexical constraints, sparse clue conjunctions, local context checks, multi-step hypothesis refinement
- Proposes Direct Corpus Interaction (DCI): agents query raw text directly via terminal tools instead of using off-the-shelf retrievers
- Introduces DCI-Agent-Lite framework for agentic corpus interaction
- Evaluates on IR benchmarks (BEIR datasets), BrowseComp-Plus, and multi-hop QA

## Method
The DCI approach:
1. Instead of calling a retriever API that returns top-k documents, the agent is given terminal-style access to the corpus
2. The agent can issue queries, browse documents, run pattern searches (grep-like), and navigate the corpus structure
3. Evidence that would be filtered out by early top-k truncation can be discovered through iterative exploration
4. The agent uses its reasoning capability to guide corpus navigation rather than relying on pre-computed similarity scores

This shifts the retrieval paradigm from "similarity matching" to "interactive corpus exploration."

## Results
- Outperforms traditional retrieval methods on complex agentic search tasks
- Particularly strong on multi-hop QA and tasks requiring sparse clue conjunction
- BEIR dataset evaluation shows improvements where exact lexical matching matters
- BrowseComp-Plus evaluation demonstrates web-scale corpus interaction capabilities

## Datasets Used
- BEIR datasets (IR benchmarks)
- BrowseComp-Plus
- Multi-hop QA datasets

## Models Released
- GitHub: https://github.com/DCI-Agent/DCI-Agent-Lite (2 stars)

## Connections
- Related: [[sources/react]] — reasoning + acting paradigm
- Related: [[sources/web2bigtable]] — bi-level multi-agent web-to-table search
- Related: [[sources/rag-survey]] — retrieval-augmented generation survey
- Related concept: [[concepts/rag]], [[concepts/agents]]

## Citation
> Li et al., "Beyond Semantic Similarity: Rethinking Retrieval for Agentic Search via Direct Corpus Interaction," arXiv:2605.05242, 2026.
