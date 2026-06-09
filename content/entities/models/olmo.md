---
type: entity
category: model
tags: [open-science, pre-training, allenai, open-source, moe]
---

# OLMo (Open Language Model)

> AllenAI's family of **fully open** language models — the first major LLM release to include training data, code, logs, and all intermediate checkpoints alongside model weights, establishing a new standard for open-science AI.

## Overview
OLMo represents a fundamentally different philosophy from other open-weight models like LLaMA or Mistral. While those projects release model weights under permissive licenses, OLMo releases the complete training pipeline: the Dolma pretraining dataset, the training code, all intermediate checkpoints, W&B training logs, and the Paloma evaluation framework. This enables true scientific reproducibility — researchers can not only use the models but understand and improve every aspect of how they were made.

## Model Family

### OLMo (v1)
| Model | Params | Training Tokens | Context | Key Feature |
|---|---|---|---|---|
| OLMo-1B | 1B | 3T (Dolma) | 2048 | Ultra-small fully open model |
| OLMo-7B | 7B | 2.46T (Dolma) | 2048 | Flagship, competitive with LLaMA-7B |
| OLMo-7B-Instruct | 7B | + Tülu SFT + DPO | 2048 | Instruction-tuned variant |

### OLMoE (Mixture of Experts)
| Model | Total Params | Active Params | Training Tokens | Key Feature |
|---|---|---|---|---|
| OLMoE-1B-7B | 6.9B | 1.3B | 5T | 64 experts, top-8 routing |
| OLMoE-1B-7B-Instruct | 6.9B | 1.3B | + Tülu 3 + DPO | Outperforms Llama2-13B-Chat |

### OLMo 2
- Improved training stability with RLVR (Reinforcement Learning with Verifiable Rewards)
- Enhanced data mixtures and longer training

## Architecture
All OLMo models follow the [[sources/llama|LLaMA template]]:
- Decoder-only Transformer
- RMSNorm (pre-normalization)
- SwiGLU activation
- RoPE positional embeddings
- No biases
- OLMoE adds: 64 fine-grained experts with top-8 routing, QK-Norm for stability

## Training Data
- [[entities/datasets/dolma|Dolma]] — 3T token open corpus (Common Crawl, Code, Academic Papers, Books, Wikipedia, Reddit)
- OLMoE-Mix — 5T tokens (DCLM + Dolma + StarCoder + peS2o + Wikipedia + Fandom)
- All data sources documented and openly released

## Benchmarks

### OLMo-7B vs. Peers
| Model | ARC-E | ARC-C | HellaSwag | PIQA | MMLU |
|---|---|---|---|---|---|
| OLMo-7B | 72.6 | 42.1 | 76.4 | 78.4 | 28.3 |
| LLaMA-7B | 72.5 | 44.5 | 77.8 | 78.5 | 33.3 |
| MPT-7B | 70.5 | 42.2 | 77.6 | 79.4 | 30.8 |

### OLMoE-1B-7B vs. Peers
| Model | Active Params | MMLU | ARC-C | HellaSwag |
|---|---|---|---|---|
| OLMoE-1B-7B | 1.3B | 52.2 | 52.1 | 79.6 |
| OLMo-7B | 7B | 52.0 | 48.5 | 78.2 |
| DeepSeekMoE-16B | 2.8B | 45.0 | 39.8 | 73.0 |

OLMoE matches OLMo-7B with 1/5 the active parameters.

## Significance
OLMo's impact goes beyond the models themselves:
1. **Reproducibility**: The only major LLM family where results can be independently verified
2. **Research enablement**: Intermediate checkpoints enable studying training dynamics
3. **Cross-platform validation**: Trained on both NVIDIA A100 and AMD MI250X GPUs
4. **Data science**: Dolma enables studying how pretraining data affects model behavior
5. **Community**: Spawned DCLM (data curation benchmark), Paloma (evaluation), Tülu (adaptation recipes)

## Related Papers
- [[sources/olmo]] — OLMo: Accelerating the Science of Language Models (ACL 2024)
- [[sources/olmo-2]] — OLMo 2: Improved architecture, Dolmino Mix, Tülu 3 post-training
- [[sources/olmo-3]] — OLMo 3: Strongest fully-open thinking model (7B, 32B)
- [[sources/olmoe]] — OLMoE: Open Mixture-of-Experts Language Models
- [[sources/tulu-3]] — Tülu 3: Post-training recipe (SFT + DPO + RLVR)
- [[sources/dolma]] — Dolma: 3T token open pretraining corpus
- [[sources/pythia]] — Pythia: Inspired OLMo's open-checkpoint approach

## See Also
- [[entities/orgs/allenai]] — AllenAI (creator)
- [[entities/datasets/dolma]] — Dolma pretraining dataset
- [[concepts/pre-training]] — Pre-training methodology
- [[concepts/mixture-of-experts]] — MoE architecture (OLMoE)
- [[concepts/training-infrastructure]] — Cross-platform training