---
type: source
arxiv_id: "2504.03624"
title: "Nemotron-H: A Family of Accurate and Efficient Hybrid Mamba-Transformer Models"
authors: ["NVIDIA"]
date: 2025-04-04
org: "NVIDIA"
tags: [architecture, hybrid, mamba, efficiency, 2025]
upvotes: 18
---

# Nemotron-H: Hybrid Mamba-Transformer

> NVIDIA's family of **hybrid Mamba-Transformer** models (8B and 56B/47B) that replace the majority of self-attention layers with **Mamba-2 layers** — achieving equivalent accuracy to Qwen 2.5 and Llama 3.1 while being **up to 3× faster** at inference. Introduces **MiniPuzzle** compression and **FP8 training** at scale.

## Key Contributions
- **Hybrid architecture**: ~92% Mamba-2 layers + ~8% attention layers — constant memory per token for most layers
- **Equivalent accuracy**: Matches Qwen2.5-7B/72B and Llama-3.1-8B/70B on standard benchmarks
- **Up to 3× faster inference**: Mamba layers provide constant computation per generated token vs. linear for attention
- **MiniPuzzle**: Novel compression technique combining pruning + NAS + distillation — 56B→47B with minimal quality loss
- **FP8 training recipe**: Full FP8 pretraining of 56B model achieving BF16-equivalent quality
- **VLM variants**: Nemotron-H-8B-VLM and 56B-VLM with strong multimodal capabilities

## Architecture
| Feature | Nemotron-H-8B | Nemotron-H-56B | Nemotron-H-47B |
|---|---|---|---|
| Total params | 8B | 56B | 47B (compressed) |
| Layers | 52 | 80 | ~68 |
| Mamba-2 layers | 48 (~92%) | 72 (~90%) | ~60 |
| Attention layers | 4 (~8%) | 8 (~10%) | ~8 |
| Training tokens | 15T | 20T | + distillation |

Key design: Attention layers placed every ~12 Mamba layers to provide global context mixing. This ratio (~8% attention) balances quality with inference speed.

## Results
### Base Models (8B class)
| Model | MMLU-Pro | ARC-C | GSM8K | HumanEval | Avg |
|---|---|---|---|---|---|
| **Nemotron-H-8B** | **34.3** | 61.6 | **83.5** | **56.7** | Strong |
| Qwen2.5-7B | 33.5 | 58.0 | 82.6 | 52.4 | Similar |
| Llama-3.1-8B | 28.3 | 54.6 | 56.5 | 37.2 | Below |

### Inference Speed
| Model | Throughput (tokens/s) | vs. Transformer |
|---|---|---|
| Nemotron-H-56B | ~3× Llama-3.1-70B | 3× faster |
| Nemotron-H-47B | ~3.6× Llama-3.1-70B | 3.6× faster |
| Nemotron-H-8B | ~2.4× Llama-3.1-8B | 2.4× faster |

## MiniPuzzle Compression
1. **Importance estimation**: Score each layer and FFN neuron
2. **Conditional NAS**: Find architecture meeting memory constraints (e.g., fit on RTX 5090 32GB)
3. **Distillation**: Retrain compressed model using logit distillation from 56B original
4. Result: 56B→47B with <1% quality loss, 20% faster, fits on consumer GPU

## Significance
Nemotron-H validates that **hybrid SSM-Transformer** architectures are production-ready:
- Mamba handles most of sequence processing at constant cost
- Strategic attention layers preserve global reasoning
- Compatible with standard post-training (SFT, RL, reasoning)
- FP8 training at 56B scale works

## Connections
- Related: [[sources/mamba|Mamba]] (SSM foundation), [[sources/llama-nemotron|Llama-Nemotron]] (reasoning)
- Concepts: [[concepts/state-space-models|SSMs]], [[concepts/llm-serving|Inference]]
- Architecture: Hybrid approach similar to [[sources/jamba|Jamba]] but with different ratio

## Citation
> NVIDIA, "Nemotron-H: A Family of Accurate and Efficient Hybrid Mamba-Transformer Models," arXiv:2504.03624, 2025.
