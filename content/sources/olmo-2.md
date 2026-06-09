---
type: source
arxiv_id: "2501.00656"
title: "OLMo 2: Furious"
authors: ["Team OLMo", "Pete Walsh", "Luca Soldaini", "et al."]
date: 2025-01-01
org: "AllenAI"
tags: [open-science, pre-training, alignment, rlvr, 2025]
upvotes: 22
---

# OLMo 2

> The next generation of AllenAI's **fully open language models** — with improved architecture (RMSNorm, QK-Norm, increased RoPE θ), a novel mid-training curriculum (Dolmino Mix 1124), and [[sources/tulu-3|Tülu 3]] post-training. OLMo 2-13B matches or surpasses Llama 3.1 and Qwen 2.5 at equivalent scale while being **fully open** (data + code + logs + checkpoints).

## Key Contributions
- **Training stability improvements**: QK-Norm, proper initialization, RMSNorm, AdamW ε=10⁻⁸ — eliminated loss spikes that plagued OLMo 1
- **Dolmino Mix 1124**: Specialized mid-training data mix with high-quality web, math, code, and curated sources for annealing phase
- **Checkpoint soups**: Averaging multiple mid-training checkpoints for improved robustness
- **Fully open**: All artifacts released — model weights, training data, code, recipes, logs, intermediate checkpoints
- **Two scales**: 7B (4T tokens) and 13B (5T tokens)

## Architecture Improvements (vs. OLMo 1)
| Feature | OLMo 1 | OLMo 2 |
|---|---|---|
| Normalization | Non-parametric LayerNorm | **RMSNorm** |
| QKV Normalization | None/Clip to 8 | **QK-Norm** |
| RoPE θ | 10⁴ | **5×10⁵** (longer context) |
| Initialization | muP-inspired | **Normal distribution (std=0.02)** |
| AdamW ε | 10⁻⁵ | **10⁻⁸** |

Core architecture remains: SwiGLU, no biases, GQA, pre-normalization.

## Training Recipe
1. **Stage 1 (Stable pretraining)**: ≥90% of training on broad web data (DCLM, Dolma)
2. **Stage 2 (Mid-training/Annealing)**: Dolmino Mix 1124 — high-quality curated data with learning rate decay
   - Filtered DCLM (51.9%), FLAN (11.3%), peS2o (academic, 19.4%), math (MathCoder, synthetic), code, Wikipedia
3. **Post-training**: [[sources/tulu-3|Tülu 3]] recipe — SFT → DPO → RLVR (with permissive data focus)

### Training Stability Deep Dive
Key finding: **Repeated n-gram sequences** in training data cause gradient/loss spikes. OLMo 2 addresses this through:
- Data filtering for repeated n-grams
- QK-Norm to bound attention logits
- Proper initialization distribution
- Higher RoPE base frequency for better long-range attention

## Results

### Base Models
| Model | FLOPs (×10²³) | MMLU | ARC-C | HellaSwag | GSM8K | Avg |
|---|---|---|---|---|---|---|
| OLMo 2 7B | 3.5 | 63.7 | 53.3 | 80.3 | 68.1 | Strong |
| Llama 3.1 8B | 9.4 | 65.2 | 53.5 | 78.9 | 56.5 | Similar |
| Qwen 2.5 7B | — | 74.2 | 55.0 | 80.3 | 82.9 | Stronger |
| OLMo 2 13B | 9.7 | 67.5 | 56.3 | 83.1 | 73.3 | Strong |
| Llama 3.1 8B | 9.4 | 65.2 | 53.5 | 78.9 | 56.5 | Below OLMo2-13B |

OLMo 2 sits at the Pareto frontier of performance vs. compute for fully open models.

### Instruct Models
OLMo 2-Instruct is competitive with or surpasses Qwen 2.5, Llama 3.1, and Gemma 2 instruct variants at comparable sizes.

## Significance
1. **New open-science standard**: First time a fully open model matches closed-recipe models at 7B and 13B scales
2. **Reproducibility**: Thousands of intermediate checkpoints released for studying training dynamics
3. **Infrastructure**: Trained on two Ai2 clusters (Jupiter + Augusta) with detailed operations documentation
4. **Environmental transparency**: Full carbon footprint analysis published

## Connections
- Builds on: [[sources/olmo|OLMo]] (v1), [[sources/tulu-3|Tülu 3]] (post-training)
- Uses: [[entities/datasets/dolma|Dolma]], [[entities/datasets/dclm|DCLM]]
- Related: [[entities/models/olmo|OLMo model family]], [[entities/orgs/allenai|AllenAI]]
- Concepts: [[concepts/pre-training]], [[concepts/training-infrastructure]]

## Citation
> Team OLMo et al., "OLMo 2: Furious," arXiv:2501.00656, 2025.
