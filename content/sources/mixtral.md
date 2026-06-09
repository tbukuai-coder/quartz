---
type: source
arxiv_id: "2401.04088"
title: "Mixtral of Experts"
authors: ["Albert Q. Jiang", "Alexandre Sablayrolles", "Antoine Roux", "et al."]
date: 2024-01-08
org: "Mistral AI"
tags: [open-models, moe, architecture, 2024]
upvotes: 160
---

# Mixtral of Experts (Mixtral 8x7B)

> A **Sparse Mixture of Experts** model where each token uses only 2 of 8 experts per layer — accessing 47B total parameters but using only 13B active parameters, matching Llama 2 70B while being 6× faster at inference.

## Key Contributions
- Demonstrated that **sparse MoE** can dramatically improve the quality-to-compute ratio
- Each token accesses 47B parameters but only uses ~13B active — same inference cost as a 13B dense model
- Outperforms Llama 2 70B on most benchmarks while being 6× faster
- Matches or exceeds GPT-3.5 on most benchmarks
- Released Mixtral 8x7B Instruct fine-tuned via DPO

## Method
Same architecture as [[sources/mistral-7b]] except each feed-forward block is replaced by **8 expert FFN blocks** with a **router network**:
- Router selects **top-2 experts** per token per layer
- Expert outputs are combined via weighted sum (router logits as weights)
- 32 layers × 8 experts = 256 expert blocks total
- SWA and GQA retained from Mistral 7B
- Context length: 32K tokens

The instruct version uses **DPO** alignment (not RLHF/PPO), indicating the shift toward simpler alignment methods in the ecosystem.

## Results
- Outperforms **Llama 2 70B** on most benchmarks (using 6× less compute)
- Matches **GPT-3.5** on standard benchmarks
- Strong performance on math, code generation, and multilingual tasks
- Mixtral Instruct achieves 8.30 on MT-Bench (vs. GPT-3.5's 8.32)

## Connections
- **Builds on**: [[sources/mistral-7b]] (base architecture), [[sources/dpo]] (alignment)
- **Key concepts**: [[concepts/mixture-of-experts]], [[concepts/gqa]], [[concepts/swa]], [[concepts/dpo]]
- **Models**: [[entities/models/mistral]]
- **Organizations**: [[entities/orgs/mistral-ai]]

## Citation
> Jiang et al., "Mixtral of Experts," arXiv:2401.04088, 2024.
> https://huggingface.co/papers/2401.04088
