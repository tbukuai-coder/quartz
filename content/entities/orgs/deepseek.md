---
type: entity
category: org
tags: [deepseek, reasoning, open-models, moe]
---

# DeepSeek

> Chinese AI lab that pioneered **RL-based reasoning** and **cost-efficient frontier training** — introducing GRPO, MLA, and producing DeepSeek-V3 ($5.5M) + DeepSeek-R1 (matching o1). 102K+ GitHub stars.

## Key Contributions
- [[sources/deepseek-llm|DeepSeek LLM]] — Foundation: scaling law study, 7B/67B base models surpassing LLaMA-2-70B
- [[sources/deepseek-v3|DeepSeek-V3]] — 671B MoE trained for $5.5M; pioneered aux-loss-free routing, MLA, multi-token prediction, FP8 training
- [[sources/deepseek-r1|DeepSeek-R1]] — first open model matching o1-level reasoning via GRPO
- **GRPO** — Group Relative Policy Optimization, simplifying PPO for alignment
- **Multi-head Latent Attention** — 93% KV cache reduction for efficient MoE inference
- Showed that pure RL (without SFT) can produce emergent reasoning
- Open-sourced everything under MIT license — including distilled versions in Qwen/Llama bases

## Papers in This Wiki
- [[sources/deepseek-llm]] — Foundation: scaling laws and 7B/67B models
- [[sources/deepseek-v3]] — V3 architecture and training
- [[sources/deepseekmath]] — GRPO and mathematical reasoning
- [[sources/deepseek-r1]] — RL-based reasoning

## See Also
- [[entities/models/deepseek]]
- [[concepts/grpo]]
- [[concepts/mixture-of-experts]]
- [[concepts/scaling-laws]]
