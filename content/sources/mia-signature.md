---
type: source
arxiv_id: "2605.06416"
title: "MiA-Signature: Approximating Global Activation for Long-Context Understanding"
authors:
  - Yuqing Li
  - Jiangnan Li
  - Mo Yu
  - Zheng Lin
  - Weiping Wang
  - Jie Zhou
venue: arXiv
year: 2026
month: 5
date: "2026-05"
upvotes: 35
tags:
  - long-context
  - rag
  - agents
  - cognitive-science
  - memory
  - activation-patterns
---

# MiA-Signature: Approximating Global Activation for Long-Context Understanding

## One-Line Summary

Cognitive-science-inspired compressed representation of global activation patterns in LLMs, using submodular-based selection of high-level concepts to approximate full memory states for improved long-context understanding in RAG and agentic systems.

## Key Contributions

1. **Cognitive-science perspective on memory access** — Models LLM memory access as two-stage process: global activation over semantic memory space → compact representation for downstream processing. Inspired by "global ignition" and "partially accessible consciousness" in cognitive science.
2. **Mindscape Activation Signature (MiA-Signature)** — Compact, query-conditioned global state approximating the memory region activated by a query. Not a summary of the source, but a surrogate of the activated context.
3. **Submodular-based construction** — Greedy selection of high-level memory units maximizing coverage of activated region, with query relevance, diversity, and redundancy avoidance.
4. **Dual retriever design** — $\mathcal{E}_1$ (query-only) for initial activation view; $\mathcal{E}_2$ (mindscape-aware) conditioned on both query and current MiA-Signature, enabling evolving retrieval.
5. **Two settings** — Static signature-augmented RAG (fixed conditioning signal) and dynamic agent memory (evolving global state updated alongside local evidence).

## Method

### Core Concepts

**Mindscape**: Organized memory substrate $\mathcal{M}(D) = \{m_1, \ldots, m_N\}$ with redundancy, overlap, and multiple abstraction levels.

**Activation**: Query-induced activation $a_q: \mathcal{M}(D) \to \mathbb{R}_{\geq 0}$ measuring how strongly each memory unit belongs to the activated region.

**MiA-Signature**: Compact subset of high-level memory units $\mathcal{H}_q$:
$$\sigma^*(q) = \arg\max_{\sigma \subseteq \mathcal{H}_q, |\sigma| \leq K} \mathcal{F}(\sigma; q, \mathcal{H}_q)$$
where $\mathcal{F}$ scores relevance to query, coverage of activated region, and diversity.

### Construction Algorithm

**Step 0: Submodular Initialization**
1. Query-only retrieval ($\mathcal{E}_1$): top-$K_0=50$ fine-grained evidence units
2. Map to high-level memory units $\mathcal{H}_0(q)$
3. Greedy coverage-aware selection (vs. simple First-K truncation) to maximize joint representation of activated region

**Static RAG Integration**
- Second retrieval pass with $\mathcal{E}_2$ using $(q_t, \sigma_t)$ pair
- Retrieval score: $s(c|q,\sigma) = (1-\alpha)s_{\text{qry}}(c|q) + \alpha s_{\text{sig}}(c|\sigma)$
- Signature provides global conditioning; retrieved evidence provides local grounding

**Dynamic Agent Memory**
- Signature $\sigma_t$ evolves as new evidence is consolidated
- Updated alongside local evidence memory at each agent step
- Enables tracking of changing views of activated memory region

## Results

Evaluated on long-context understanding tasks. Consistent performance gains across:
- **RAG pipelines**: Improved retrieval relevance and generation coherence
- **Agentic systems**: Better memory-driven reasoning in multi-turn interactions

Key finding: Approximating global activation provides more effective memory interface than relying solely on local retrieval, especially for complex multi-hop reasoning.

## Connections

- **Cognitive Science Bridge**: Connects LLM memory systems to cognitive theories of consciousness (global workspace theory, partial access). Complements [[sources/compliance-vs-sensibility|Compliance vs Sensibility]]'s steering-based controllability with a memory-based perspective.
- **RAG Evolution**: Moves beyond [[concepts/rag|naive RAG]] (query → retrieve → generate) to activation-aware retrieval (query → activate → represent → retrieve → generate). Related to [[sources/dci-agent-retrieval|DCI Agent]]'s direct corpus interaction but from a representation-learning angle.
- **Long-Context**: Complements [[concepts/long-context|context extension methods]] (YaRN, LongRoPE, Mamba) by addressing how to *interface* with long memory rather than just fit more tokens into context.
- **Agent Memory**: Provides theoretical foundation for [[sources/eywa|Eywa]]'s heterogeneous scientific agent collaboration and [[sources/web2bigtable|Web2BigTable]]'s internet-scale agent memory, formalizing the "global state" that agents maintain.
- **Submodular Optimization**: Greedy coverage-aware selection shares mathematical foundations with [[sources/reasoning-vectors|Reasoning Vectors]]' task arithmetic and [[sources/trees-to-flows|Trees to Flows]]' structured optimization.

## Citation

```bibtex
@article{li2026miasignature,
  title={MiA-Signature: Approximating Global Activation for Long-Context Understanding},
  author={Li, Yuqing and Li, Jiangnan and Yu, Mo and Lin, Zheng and Wang, Weiping and Zhou, Jie},
  journal={arXiv preprint arXiv:2605.06416},
  year={2026}
}
```

---
*Ingested in Batch 26 (2026-05-05)* | [[index]] | [[concepts/long-context]] | [[concepts/rag]] | [[concepts/agents]]