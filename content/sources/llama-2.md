---
type: source
arxiv_id: "2307.09288"
title: "Llama 2: Open Foundation and Fine-Tuned Chat Models"
authors: ["Hugo Touvron", "Louis Martin", "Kevin Stone", "et al."]
date: 2023-07-18
org: "Meta AI"
tags: [open-models, alignment, rlhf, 2023]
upvotes: 251
---

# Llama 2: Open Foundation and Fine-Tuned Chat Models

> Released open pre-trained and **RLHF-aligned chat models** (7B–70B), with detailed documentation of the alignment process, setting the standard for open-source chat LLMs.

## Key Contributions
- Released both **base models** and **chat-optimized models** (Llama 2-Chat) openly
- Provided the most detailed public description of an RLHF pipeline at that time
- Introduced **Ghost Attention (GAtt)** for multi-turn dialogue consistency
- Showed Llama 2-Chat approaches closed-source models on human evaluations
- 40% more training data than LLaMA 1; 2T tokens of public data
- Trained with context length of 4096 tokens

## Method
**Pre-training**: Standard autoregressive LM on 2T tokens of public data. Same architecture as LLaMA with minor changes.

**Alignment pipeline** (for Llama 2-Chat):
1. **SFT**: Fine-tune on ~27K high-quality instruction-response demonstrations
2. **RLHF**: Two separate reward models — one for helpfulness, one for safety
3. **Rejection sampling**: Generate K responses, rank with reward model, fine-tune on best
4. **PPO**: Further optimize against reward models
5. **Ghost Attention**: Prepend system prompt to all turns during training to maintain instruction adherence across multi-turn conversations

## Models Released
| Model | Params | Context | Chat Version |
|---|---|---|---|
| Llama-2-7B | 7B | 4096 | ✅ |
| Llama-2-13B | 13B | 4096 | ✅ |
| Llama-2-70B | 70B | 4096 | ✅ |

## Connections
- **Builds on**: [[sources/llama]], [[sources/instructgpt]] (RLHF pipeline)
- **Influenced**: [[sources/mistral-7b]], [[sources/zephyr]], [[sources/gemma]], open-source alignment ecosystem
- **Key concepts**: [[concepts/rlhf]], [[concepts/pre-training]], [[concepts/instruction-tuning]]
- **Models**: [[entities/models/llama]]
- **Organizations**: [[entities/orgs/meta]]

## Citation
> Touvron et al., "Llama 2: Open Foundation and Fine-Tuned Chat Models," arXiv:2307.09288, 2023.
> https://huggingface.co/papers/2307.09288
