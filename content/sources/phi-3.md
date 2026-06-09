---
type: source
arxiv_id: "2404.14219"
title: "Phi-3 Technical Report: A Highly Capable Language Model Locally on Your Phone"
authors: ["Marah Abdin", "Sam Ade Jacobs", "et al."]
date: 2024-04-22
org: "Microsoft"
tags: [small-model, synthetic-data, on-device, 2024]
upvotes: 260
---

# Phi-3: A Highly Capable Language Model Locally on Your Phone

> A **3.8B parameter model** that rivals **Mixtral 8x7B** and **GPT-3.5** — achieving 69% on MMLU and 8.38 on MT-bench while being small enough for **on-device deployment** (phones). The innovation is entirely in the training data: heavily filtered web data + synthetic data. **260 upvotes** — among the most upvoted papers on HF.

## Key Contributions
- **3.8B rivals Mixtral 8x7B**: Data quality > model size, proven at scale
- **On-device deployment**: Runs on mobile phones (4-bit quantized: ~1.8GB)
- **Data is everything**: Same architecture as Phi-2, but data pipeline innovation drives all quality gains
- **Phi-3 family**: mini (3.8B), small (7B), medium (14B) — all competitive above weight class
- **260 upvotes**: Among most popular papers on HF Papers

## Model Family
| Model | Params | MMLU | MT-Bench | Context | Key Feature |
|---|---|---|---|---|---|
| Phi-3-mini | 3.8B | 69.0% | 8.38 | 4K/128K | Phone-deployable |
| Phi-3-small | 7B | 75.3% | 8.70 | 8K/128K | Strong mid-size |
| Phi-3-medium | 14B | 78.0% | 8.90 | 4K/128K | Best quality |

## Method
### Data Pipeline (Key Innovation)
The entire quality gain comes from data:
1. **Heavily filtered web data**: Aggressive quality filtering of Common Crawl
2. **Synthetic data**: LLM-generated data targeting specific reasoning skills (math, code, logic)
3. **Data curriculum**: Staged training mixing web and synthetic data
4. **Scaling Phi-2's recipe**: Same data philosophy as Phi-2, scaled up

### Architecture
Standard decoder-only Transformer (same as Llama):
- RMSNorm, SwiGLU, RoPE, GQA
- No architectural innovations — data is the differentiator

## Results
| Model | Params | MMLU | HumanEval | MATH | GSM8K |
|---|---|---|---|---|---|
| **Phi-3-mini** | **3.8B** | **69.0%** | **58.5%** | — | **82.5%** |
| Mixtral 8x7B | 47B (13B active) | 70.6% | — | — | 74.4% |
| GPT-3.5 | ~175B | 70.0% | 48.1% | — | 57.1% |
| Llama-3-8B | 8B | 66.6% | — | — | 79.6% |

Phi-3-mini matches models 4–12× larger.

## Impact
- Proved **data quality > model size** at the 3B scale
- Influenced [[sources/phi-4|Phi-4]] (50+ synthetic dataset types for pretraining)
- Demonstrated viable on-device LLM deployment
- Part of the "small but mighty" trend alongside [[sources/smollm2|SmolLM2]], Gemma 2B

## Connections
- Extended by: [[sources/phi-4|Phi-4]]
- Models: [[entities/models/phi|Phi family]]
- Org: [[entities/orgs/microsoft|Microsoft]]
- Related: [[sources/smollm2|SmolLM2]] (similar philosophy), [[concepts/synthetic-data]]
- Comparisons: [[comparisons/small-language-models]]

## Citation
> Abdin et al., "Phi-3 Technical Report," arXiv:2404.14219, 2024.
