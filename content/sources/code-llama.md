---
type: source
arxiv_id: "2308.12950"
title: "Code Llama: Open Foundation Models for Code"
authors: ["Baptiste Rozière", "Jonas Gehring", "et al."]
date: 2023-08-24
org: "Meta AI"
tags: [open-models, code, pre-training, 2023]
upvotes: 29
---

# Code Llama: Open Foundation Models for Code

> Specialized code models (7B–34B) based on Llama 2 with **infilling capabilities**, **100K context**, and SOTA open-source code generation — demonstrating the value of domain-specific continued pre-training.

## Key Contributions
- Released code-specialized models at 7B, 13B, and 34B scales
- Introduced **infilling capability** (fill-in-the-middle) — useful for code completion in IDEs
- Extended context to **100K tokens** through long-context fine-tuning
- Released three flavors: foundation (Code Llama), Python-specialized, and instruction-following
- SOTA among open models on HumanEval and MBPP at release

## Method
### Training Pipeline
1. Start from **Llama 2** base models
2. **Continued pre-training** on 500B tokens of code-heavy data
3. **Python specialization** (optional): additional 100B tokens of Python
4. **Long-context fine-tuning**: extend from 4K to 100K context
5. **Instruction fine-tuning** (Instruct variant): SFT on coding instructions

### Infilling
- Trained with a **causal infilling objective**: given prefix and suffix, generate the middle
- Enables IDE-style code completion (cursor in the middle of code)
- Only 7B and 13B models have infilling — 34B is autoregressive only

## Models Released
| Model | Params | Context | Infilling | HumanEval |
|---|---|---|---|---|
| Code Llama | 7B/13B/34B | 100K | ✅ (7B/13B) | 33.5–53.7% |
| Code Llama Python | 7B/13B/34B | 100K | ❌ | 38.4–57.0% |
| Code Llama Instruct | 7B/13B/34B | 100K | ✅ (7B/13B) | 34.8–67.8% |

## Connections
- **Builds on**: [[sources/llama-2]] (base model)
- **Key concepts**: [[concepts/pre-training]], [[concepts/fine-tuning]], [[concepts/instruction-tuning]]
- **Related**: Qwen2.5-Coder ([[sources/qwen25]]), DeepSeek-Coder ([[entities/models/deepseek]])
- **Organizations**: [[entities/orgs/meta]]

## Citation
> Rozière et al., "Code Llama: Open Foundation Models for Code," arXiv:2308.12950, 2023.
> https://huggingface.co/papers/2308.12950
