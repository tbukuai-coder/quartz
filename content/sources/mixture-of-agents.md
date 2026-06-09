---
type: source
arxiv_id: "2406.04692"
title: "Mixture-of-Agents Enhances Large Language Model Capabilities"
authors: ["Junlin Wang", "Jue Wang", "Ben Athiwaratkun", "Ce Zhang", "James Zou"]
date: 2024-06-07
org: "Together AI / Stanford"
tags: [multi-agent, inference, ensemble, alignment, 2024]
upvotes: 59
---

# Mixture-of-Agents (MoA)

> A layered multi-agent architecture where each LLM refines its response using outputs from other LLMs in the previous layer, achieving state-of-the-art on AlpacaEval 2.0.

## Key Contributions
- Introduced **Mixture-of-Agents (MoA)**, a layered architecture where multiple LLMs collaborate iteratively
- Achieved **65.1% on AlpacaEval 2.0** (LC win rate), surpassing GPT-4o at the time of publication
- Discovered the **collaborativeness** property: most LLMs generate better responses when given reference outputs from other models
- Demonstrated that **open-source LLMs can collectively surpass proprietary frontier models** through intelligent orchestration
- Released open-source implementation via Together AI

## Method
MoA organizes LLMs in **layers**. In each layer, multiple LLM "agents" generate responses to the same prompt. Each agent also sees the responses from all agents in the previous layer as auxiliary context. This iterative refinement progressively improves quality.

Key design: agents are categorized as **proposers** (good at generating diverse initial responses) or **aggregators** (good at synthesizing and refining). The final layer uses a single aggregator to produce the output.

Typical setup: 3 layers with 6 agents per layer, using a mix of Qwen, LLaMA, Mixtral, and other open models.

## Results
- **AlpacaEval 2.0**: 65.1% LC win rate (vs GPT-4o's 57.5% at the time)
- **MT-Bench**: 9.25 average score
- **FLASK**: Significant gains across all fine-grained quality dimensions
- Performance scales with more layers and more agents (diminishing returns after ~3 layers)
- Even weaker models contribute meaningfully as proposers

## Connections
- **Builds on**: [[sources/llama-3|Llama 3]], [[sources/qwen25|Qwen2.5]], [[sources/mixtral|Mixtral]] (as component agents)
- **Related**: [[sources/malt|MALT]] (multi-agent training), [[concepts/agents|LLM Agents]]
- **Published by**: [[entities/orgs/together-ai|Together AI]]
- **Influenced**: Multi-agent inference becoming a practical deployment pattern
- **Related concepts**: [[concepts/llm-evaluation|LLM Evaluation]] (AlpacaEval, MT-Bench), [[concepts/mixture-of-experts|Mixture of Experts]] (similar name, different concept)

## Citation
> Wang et al., "Mixture-of-Agents Enhances Large Language Model Capabilities," arXiv:2406.04692, 2024.
