---
type: entity
category: model
tags: [open-models, deepseek, reasoning, moe, mla]
---

# DeepSeek Models

> DeepSeek's model family — pioneering **RL-based reasoning**, efficient MoE architecture, and achieving frontier performance with open weights. DeepSeek-V3.2 surpasses GPT-5 on reasoning; DeepSeekMath-V2 achieves IMO-level self-verifiable math reasoning.

## Overview
DeepSeek, a Chinese AI lab, has produced some of the most impactful open-source models. Their innovations span architecture (MLA, DeepSeekMoE, DSA), training efficiency (FP8, auxiliary-loss-free routing), alignment (GRPO for reasoning), and formal math (self-verifiable proofs). DeepSeek-V3.2 surpasses GPT-5 and Gemini-3.0-Pro on complex reasoning.

## Models

| Model | Year | Params | Active | Key Innovation |
|---|---|---|---|---|
| DeepSeek LLM 7B/67B | 2024 | 7B–67B | All | Foundation models, scaling law study |
| DeepSeek-Coder-V1.5 | 2023 | 7B–33B | All | Code-specialized base |
| DeepSeekMath 7B | 2024 | 7B | All | Introduced GRPO; 51.7% on MATH |
| DeepSeek-V2 | 2024 | 236B | 21B | Introduced MLA + DeepSeekMoE |
| **DeepSeek-V3** | 2024 | **671B** | **37B** | MLA + aux-loss-free + MTP; trained for **$5.5M** |
| DeepSeek-R1 | 2025 | 671B | 37B | Full pipeline reasoning; matches o1 |
| DeepSeekMath-V2 | 2025 | — | — | Self-verifiable math reasoning; IMO/CMO/Putnam |
| DeepSeek-Prover-V2 | 2025 | — | — | Formal theorem proving in Lean 4 |
| **DeepSeek-V3.2** | 2025 | **671B** | **37B** | DSA + scalable RL; **surpasses GPT-5** |

## Key Architectural Innovations
- **Multi-head Latent Attention (MLA)**: Compresses KV cache by 93%
- **DeepSeek Sparse Attention (DSA)**: V3.2 — efficient attention for long contexts
- **DeepSeekMoE**: 256 routed experts + shared experts per layer
- **Auxiliary-loss-free load balancing**: Dynamic bias for expert routing
- **Multi-Token Prediction**: Densifies training signals
- **FP8 training**: First at frontier scale
- **GRPO**: Eliminates critic model from PPO — [[concepts/grpo]]

## Related Papers
- [[sources/deepseek-llm]] — Foundation: scaling laws and 7B/67B base models
- [[sources/deepseek-v3]] — V3 architecture and training
- [[sources/deepseek-v32]] — V3.2: DSA + scalable RL, surpasses GPT-5
- [[sources/deepseekmath]] — GRPO and math reasoning
- [[sources/deepseekmath-v2]] — Self-verifiable mathematical reasoning
- [[sources/deepseek-r1]] — RL-based reasoning
- [[sources/deepseek-prover-v2]] — Formal theorem proving

## See Also
- [[entities/orgs/deepseek]]
- [[concepts/grpo]]
- [[concepts/mixture-of-experts]]
- [[concepts/scaling-laws]]
