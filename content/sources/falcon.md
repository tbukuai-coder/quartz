---
type: source
arxiv_id: "2311.16867"
title: "The Falcon Series of Open Language Models"
authors: ["Ebtesam Almazrouei", "Hamza Alobeidli", "Abdulaziz Alshamsi", "et al."]
date: 2023-11-28
org: "TII"
tags: [open-models, pre-training, web-data, 2023]
upvotes: 15
---

# The Falcon Series of Open Language Models

> Introduced the **Falcon series** (7B, 40B, 180B parameters) — trained predominantly on [[sources/refinedweb|RefinedWeb]] (web-only data), demonstrating that properly filtered web data can produce frontier-competitive models. Falcon-180B trained on **3.5 trillion tokens** across up to **4,096 A100 GPUs**, nearing PaLM-2-Large performance.

## Key Contributions
- **Web-data-only thesis validated at scale**: ~85% web data (RefinedWeb) can match curated multi-source corpora
- **Largest documented pretraining run**: 3.5T tokens for Falcon-180B, the largest openly documented training run at the time
- **Multi-group attention**: Extended multi-query to multi-group (GQA variant) for tensor-parallel inference
- **Cloud-scale training**: Custom Gigatron codebase for training on up to 4,096 A100s on AWS cloud
- **Extensive ablations**: Thorough 1B/3B ablation study validating data, architecture, and hyperparameter choices

## Method
### Data — Predominantly Web
- **76% RefinedWeb-English** + **8% RefinedWeb-Euro** (multilingual) = 84% web data
- **6% Books** (Project Gutenberg), **5% Conversations** (Reddit, SO), **3% Code** (GitHub), **2% Technical** (arXiv, Wikipedia)
- **No upsampling** of any source — conservative approach to avoid memorization/degradation
- Total dataset: 3,500B tokens designed for the compute budget

### Architecture
- Decoder-only Transformer with:
  - Multi-query attention (7B) / Multi-group attention with 8 KV heads (40B, 180B)
  - Parallel attention + MLP (GPT-J style) for throughput
  - RoPE positional embeddings (validated over ALiBi in ablations)
  - LayerNorm, no biases
- Custom Gigatron distributed training framework on AWS p4d instances

### Key Ablation Findings
1. **Web-only ≥ curated**: RefinedWeb alone matches The Pile on downstream tasks
2. **Code and multilingual**: Small amounts (3–8%) improve English performance
3. **Multi-group attention**: No performance degradation vs. multi-head, significant inference speedup
4. **Parallel attention+MLP**: ~10% throughput improvement with no quality loss

## Results
| Model | MMLU (5-shot) | HellaSwag | ARC-C | vs. Peers |
|---|---|---|---|---|
| Falcon-7B | 26.2 | 78.1 | 47.9 | Competitive with LLaMA-7B |
| Falcon-40B | 55.4 | 85.3 | 61.0 | #1 HF Leaderboard (briefly) |
| Falcon-180B | 70.4 | 88.0 | 69.4 | Near PaLM-2-Large, above LLaMA 2 70B |

## Connections
- Data: [[sources/refinedweb|RefinedWeb]]
- Models: [[entities/models/falcon|Falcon family]]
- Org: [[entities/orgs/tii|TII]]
- Concepts: [[concepts/pre-training]], [[concepts/gqa|GQA]], [[concepts/positional-encodings|RoPE]]
- Comparisons: [[comparisons/open-model-families]], [[comparisons/pretraining-data]]

## Citation
> Almazrouei et al., "The Falcon Series of Open Language Models," arXiv:2311.16867, 2023.
