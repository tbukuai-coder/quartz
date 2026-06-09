---
type: source
arxiv_id: "2412.15115"
title: "Qwen2.5 Technical Report"
authors: ["Qwen Team", "An Yang", "Baosong Yang", "et al."]
date: 2024-12-19
org: "Alibaba / Qwen"
tags: [open-models, pre-training, multilingual, 2024]
upvotes: 378
---

# Qwen2.5 Technical Report

> A comprehensive LLM series ranging from **0.5B to 72B** parameters (plus MoE variants), trained on **18 trillion tokens**, achieving performance competitive with Llama-3-405B and GPT-4o-mini.

## Key Contributions
- Scaled pre-training data from 7T (Qwen2) to **18T tokens** — the largest publicly documented
- Released models from **0.5B to 72B** parameters, plus **Qwen2.5-Turbo** and **Qwen2.5-Plus** (API)
- Qwen2.5-72B-Instruct competitive with **Llama-3-405B-Instruct** (5.6× larger)
- Strong performance in **coding**, **mathematics**, and **multilingual** tasks
- Extensive post-training: SFT + multi-stage RL (DPO and online RL)
- Open-sourced under various licenses including Apache 2.0

## Method
### Pre-training
- 18T tokens of diverse, high-quality data (web, code, math, multilingual)
- Improved data filtering and quality classification
- Careful data mixing ratios across domains
- Context length up to 128K tokens (Qwen2.5-1M extends to 1M)

### Post-training
- **SFT**: Curated instruction data across diverse tasks
- **DPO**: Preference alignment with AI-generated comparisons
- **Online RL**: Further refinement with reward model feedback
- Multi-stage process with iterative quality improvements

### Architecture
- Standard Transformer decoder with GQA
- RoPE embeddings, SwiGLU activation, RMSNorm
- MoE variant available (Qwen2.5-MoE)

## Models Released
| Model | Params | Active Params | Context |
|---|---|---|---|
| Qwen2.5-0.5B | 0.5B | 0.5B | 128K |
| Qwen2.5-1.5B | 1.5B | 1.5B | 128K |
| Qwen2.5-3B | 3B | 3B | 128K |
| Qwen2.5-7B | 7B | 7B | 128K |
| Qwen2.5-14B | 14B | 14B | 128K |
| Qwen2.5-32B | 32B | 32B | 128K |
| Qwen2.5-72B | 72B | 72B | 128K |

## Connections
- **Key concepts**: [[concepts/pre-training]], [[concepts/dpo]], [[concepts/rlhf]], [[concepts/scaling-laws]], [[concepts/gqa]]
- **Models**: [[entities/models/qwen]]
- **Organizations**: [[entities/orgs/alibaba]]
- **Used as base for**: DeepSeek-R1 distillation (Qwen2.5 variants)
- **GitHub**: [QwenLM/Qwen2.5](https://github.com/QwenLM/Qwen2.5) (27.2K ⭐)

## Citation
> Qwen Team, "Qwen2.5 Technical Report," arXiv:2412.15115, 2024.
> https://huggingface.co/papers/2412.15115
