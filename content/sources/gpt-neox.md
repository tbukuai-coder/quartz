---
type: source
arxiv_id: "2204.06745"
title: "GPT-NeoX-20B: An Open-Source Autoregressive Language Model"
authors: ["Sid Black", "Stella Biderman", "Eric Hallahan", "et al."]
date: 2022-04-14
org: "EleutherAI"
tags: [open-models, pre-training, foundational, 2022]
upvotes: 1
---

# GPT-NeoX-20B

> The **largest dense open-source model** at its release (April 2022) — a 20B parameter autoregressive LM trained on **The Pile** by [[entities/orgs/eleutherai|EleutherAI]]. Demonstrated superior few-shot reasoning vs. similarly-sized models and pioneered many architectural choices later adopted by larger models.

## Key Contributions
- **Largest open model (2022)**: 20B parameters, fully open weights and code — largest at the time
- **The Pile training**: Trained on EleutherAI's 800GB diverse English corpus
- **Architectural innovations**: Parallel attention+FFN, rotary embeddings — later adopted by LLaMA and others
- **Few-shot reasoning**: Particularly strong on math and knowledge tasks
- **Open infrastructure**: Released GPT-NeoX training library (basis for many subsequent projects)

## Architecture
- **20B parameters**: 44 layers, 6144 hidden dimension, 64 attention heads
- **Rotary Position Embeddings (RoPE)**: Early adoption of [[sources/rope|RoPE]], before LLaMA popularized it
- **Parallel attention + FFN**: Attention and FFN computed in parallel (GPT-J style) — later adopted by Falcon, PaLM
- **Tokenizer**: 50,257 BPE tokens (GPT-2 tokenizer)
- **Training**: 150B tokens from The Pile, 96 A100 40GB GPUs

## Results
| Model | Params | LAMBADA | PIQA | Winogrande | Math |
|---|---|---|---|---|---|
| **GPT-NeoX-20B** | **20B** | **71.7** | **78.0** | **66.2** | Strong |
| GPT-J-6B | 6B | 68.3 | 75.4 | 64.7 | Weaker |
| GPT-3 (13B) | 13B | ~70 | ~76 | ~64 | Weaker |
| FairSeq 13B | 13B | 68.2 | 75.7 | 64.0 | — |

Notably strong on few-shot math reasoning relative to model size.

## Legacy
GPT-NeoX-20B's impact extends beyond the model itself:
1. **GPT-NeoX library**: Open-source training framework used by many subsequent projects
2. **Architecture template**: Parallel attention+FFN and RoPE adopted by [[sources/falcon|Falcon]], PaLM
3. **Inspired Pythia**: [[sources/pythia|Pythia]] used the same GPT-NeoX architecture for controlled scaling studies
4. **Community building**: Demonstrated that volunteer researchers could train frontier-scale models
5. **Preceded BLOOM**: Released months before [[sources/bloom|BLOOM]] (176B), showing different paths to open models

## Connections
- Org: [[entities/orgs/eleutherai|EleutherAI]]
- Related: [[sources/pythia|Pythia]] (controlled scaling with same architecture)
- Architecture: [[sources/rope|RoPE]], parallel attention+FFN
- Concepts: [[concepts/pre-training]], [[concepts/scaling-laws]]

## Citation
> Black et al., "GPT-NeoX-20B: An Open-Source Autoregressive Language Model," BigScience Workshop @ ACL 2022, arXiv:2204.06745.
