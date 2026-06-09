---
type: source
arxiv_id: "2211.05100"
title: "BLOOM: A 176B-Parameter Open-Access Multilingual Language Model"
authors: ["BigScience Workshop"]
date: 2022-11-09
org: "BigScience / Hugging Face"
tags: [open-models, multilingual, collaborative, foundational, 2022]
upvotes: 37
---

# BLOOM: A 176B-Parameter Open-Access Multilingual Language Model

> The first **176B-parameter open-access multilingual model**, created by a collaboration of **hundreds of researchers** in the BigScience workshop. Trained on the **ROOTS corpus** (1.6TB, 46 natural languages + 13 programming languages) on France's Jean Zay supercomputer. Introduced the **Responsible AI License (RAIL)**.

## Key Contributions
- **Largest open model at release**: 176B parameters, fully open-access — unprecedented scale for a community project
- **Massively multilingual**: 46 natural languages + 13 programming languages with explicit fairness considerations
- **Collaborative development**: 1,000+ researchers from 60+ countries and 250+ institutions
- **ROOTS corpus**: 1.6TB composite multilingual dataset with documented provenance
- **RAIL license**: Responsible AI License model — permissive with behavioral use restrictions, widely adopted
- **BLOOMZ**: Multitask-prompted finetuning variant with strong zero-shot generalization

## Method
### Architecture
- Decoder-only Transformer (causal LM)
- **ALiBi** positional embeddings (not RoPE — pre-dates the RoPE standard)
- **Embedding LayerNorm**: Additional LayerNorm after embedding layer for training stability at 100B+ scale
- 70 layers, 14336 hidden dim, 112 attention heads
- Byte-level BPE tokenizer with 250,680 vocabulary — designed for multilingual fairness

### Training Data: ROOTS
- 498 Hugging Face datasets across 59 languages
- 30% English, 16.2% Chinese, 12.9% French, 10.8% Spanish, 10.6% code
- Language-specific working groups curated data sources
- Extensive data documentation with provenance tracking

### Training Infrastructure
- **Jean Zay supercomputer** (IDRIS/CNRS, France) — 384 A100 80GB GPUs
- Megatron-DeepSpeed for distributed training
- 3.5 months of training
- float16 (small models), bfloat16 (176B)

## Results
| Task | BLOOM-176B | OPT-175B | Notes |
|---|---|---|---|
| SuperGLUE (0-shot) | Competitive | Competitive | Strong on entailment tasks |
| WMT en→fr (1-shot) | 38.0 BLEU | 31.4 BLEU | Significantly better multilingual |
| HumanEval (pass@1) | 15.5% | 15.6% | Comparable code generation |
| MMLU (5-shot) | ~39% | ~35% | Better than OPT |

BLOOMZ (multitask finetuned) showed dramatic improvements in zero-shot task generalization across languages.

## Historical Significance
- **First open 100B+ model**: Predated LLaMA by 4 months; showed open frontier models were possible
- **RAIL license**: Template adopted by Stability AI (Stable Diffusion), Meta (Llama 2), and others
- **Multilingual priority**: Established that open models should serve diverse language communities
- **Governance model**: Working groups, ethics review, transparent documentation — template for future collaborations
- Superseded by [[sources/llama|LLaMA]] (Feb 2023) which achieved better performance at smaller scale

## Connections
- Org: [[entities/orgs/huggingface|Hugging Face]] (organizer)
- Models: [[entities/models/bloom|BLOOM family]]
- Related: [[concepts/multilingual-models]], [[concepts/tokenization]], [[concepts/pre-training]]
- Successor: [[sources/llama]] (smaller, more performant, drove the open LLM revolution)

## Citation
> BigScience Workshop, "BLOOM: A 176B-Parameter Open-Access Multilingual Language Model," arXiv:2211.05100, 2022.
