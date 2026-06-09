---
type: source
arxiv_id: "2512.02556"
title: "DeepSeek-V3.2: Pushing the Frontier of Open Large Language Models"
authors: ["DeepSeek-AI", "Aixin Liu", "Aoxue Mei"]
date: 2025-12-03
org: "DeepSeek"
tags: [open-model, reasoning, moe, frontier, agents, 2025]
upvotes: 267
---

# DeepSeek-V3.2

> DeepSeek's latest frontier model featuring DeepSeek Sparse Attention (DSA) and scalable RL, achieving superior reasoning performance compared to GPT-5 and Gemini-3.0-Pro on complex tasks.

## Key Contributions
- Introduced **DeepSeek Sparse Attention (DSA)**: efficient attention mechanism that substantially reduces computational complexity while preserving performance in long-context scenarios
- Developed a **scalable reinforcement learning framework** with agentic task synthesis pipeline — extending RL beyond math/code to general reasoning
- Achieved **gold-medal level performance** on International Mathematical Olympiad (IMO) and International Olympiad in Informatics (IOI) problems
- **Surpasses GPT-5 and Gemini-3.0-Pro** on complex reasoning benchmarks
- Maintains the cost-efficient MoE architecture from [[sources/deepseek-v3|DeepSeek-V3]]

## Method
Builds on DeepSeek-V3 architecture (671B MoE, 37B active) with key improvements:
1. **DeepSeek Sparse Attention (DSA)**: Selectively attends to relevant tokens in long sequences, reducing O(n²) attention to near-linear for long contexts without quality loss
2. **Scalable RL framework**: Extends reasoning RL beyond math/code to agentic tasks via synthetic task generation pipeline
3. **Agentic capabilities**: Optimized for multi-step reasoning, tool use, and autonomous task completion

## Results
- **AIME 2024**: Gold-medal level performance
- **IMO**: Competitive with specialized math systems
- **IOI**: Strong performance on competitive programming
- **General reasoning**: Surpasses GPT-5 and Gemini-3.0-Pro on complex multi-step tasks
- **Long-context**: DSA enables efficient processing of very long sequences

## Models Released
- DeepSeek-V3.2 (open weights, MIT license)

## Connections
- **Builds on**: [[sources/deepseek-v3|DeepSeek-V3]], [[sources/deepseek-r1|DeepSeek-R1]]
- **Part of**: [[entities/models/deepseek|DeepSeek]] family, [[entities/orgs/deepseek|DeepSeek]]
- **Related concepts**: [[concepts/mixture-of-experts|MoE]], [[concepts/grpo|GRPO]], [[concepts/agents|Agents]]
- **Competes with**: GPT-5 (OpenAI), Gemini-3.0-Pro (Google)

## Citation
> DeepSeek-AI, "DeepSeek-V3.2: Pushing the Frontier of Open Large Language Models," arXiv:2512.02556, 2025.
