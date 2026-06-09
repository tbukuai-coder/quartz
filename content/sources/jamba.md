---
type: source
arxiv_id: "2403.19887"
title: "Jamba: A Hybrid Transformer-Mamba Language Model"
authors: ["Opher Lieber", "Barak Lenz", "Hofit Bata", "Gal Cohen", "Jhonathan Osin", "Itay Dalmedigos", "Erez Safahi", "Shaked Meirom", "Yonatan Belinkov", "Shai Shalev-Shwartz", "Omri Abend", "Raz Alon", "Tomer Asida", "Amir Bergman", "Roman Glozman", "Michael Gokhman", "Avashalom Manevich", "Nir Ratner", "Noam Rozen", "Erez Shwartz", "Mor Zusman", "Yoav Shoham"]
date: 2024-03-28
org: "AI21 Labs"
tags: [architecture, moe, ssm, hybrid, long-context, 2024]
upvotes: 112
---

# Jamba: A Hybrid Transformer-Mamba Language Model

> The first production-scale hybrid architecture combining Transformer attention, Mamba SSM, and Mixture-of-Experts — 52B total params, fits on a single 80GB GPU, supports 256K context with state-of-the-art throughput.

## Key Contributions
- First production-scale hybrid model combining three complementary technologies: Transformer (attention), [[sources/mamba|Mamba]] (SSM), and [[concepts/mixture-of-experts|MoE]]
- Demonstrated that the hybrid approach yields better quality than pure Transformer or pure Mamba at the same compute budget
- Achieved 256K effective context length with strong performance on long-context benchmarks
- Designed to fit in a single 80GB GPU (52B total, 12B active) — 2× the throughput of Mixtral 8×7B and 1.5× of Llama-2-70B at comparable quality
- Released findings on training stability for SSM-MoE combinations at scale

## Method
**Jamba Block Architecture**:
Each Jamba block contains a sequence of 8 layers with a specific pattern:
- **Attention layers**: 1 out of every 8 layers uses standard multi-head attention (with RoPE is optional — Jamba works without positional embeddings)
- **Mamba layers**: 7 out of 8 layers use Mamba SSM
- **MoE**: Applied to some layers (every other layer), with top-2 routing over 16 experts
- This creates a ratio of a:m = 1:7 (attention:Mamba) within each block

**Implementation for single 80GB GPU**:
- 4 Jamba blocks = 32 layers total
- 8 attention layers (with KV cache) + 24 Mamba layers (with SSM state — much smaller)
- MoE on every other MLP: 16 experts, top-2 routing
- Total: 52B parameters, 12B active per token
- KV cache: ~10× smaller than equivalent pure Transformer at 256K context

**Key Ablation Findings**:
- **Attention:Mamba ratio**: 1:7 is optimal for quality/efficiency tradeoff
- **MoE integration with Mamba**: Works well, but requires careful stabilization
- **Stability at scale**: Large loss spikes observed; resolved by adding RMSNorm to Mamba layers (not needed at 1.3B scale, essential at 7B+)
- **Positional embeddings**: Not required — Jamba without RoPE matches Jamba with RoPE (Mamba provides implicit position)

## Results
**Academic Benchmarks**:
| Model | Active Params | HellaSwag | WinoGrande | ARC-E | ARC-C | PIQA | MMLU |
|---|---|---|---|---|---|---|---|
| Jamba | 12B | 87.1 | 82.0 | 73.5 | 64.4 | 83.2 | 67.4 |
| Mixtral 8×7B | 12.9B | 86.7 | 81.2 | 77.6 | 60.0 | 83.0 | 70.6 |
| Llama-2-70B | 70B | 87.3 | 83.7 | 54.6 | 67.3 | 82.8 | 69.8 |

Jamba matches or approaches much larger models with only 12B active parameters.

**Throughput (tokens/sec)**:
- Jamba: 2× Mixtral 8×7B throughput on long sequences
- KV cache at 256K: Jamba ~12GB vs Mixtral ~200GB+

**Long Context** (Needle-in-a-Haystack): 100% retrieval accuracy up to 256K tokens.

## Datasets Used
- Proprietary in-house dataset (text from web)
- Training on NVIDIA H100 GPUs

## Models Released
- Jamba-v0.1 (52B total, 12B active) — permissive license
- Extended by Jamba-1.5 (12B/98B variants)

## Connections
- Builds on: [[sources/mamba|Mamba]] (SSM component), [[sources/mixtral|Mixtral]] (MoE inspiration), [[concepts/transformer-architecture|Transformer]] (attention component)
- Extended by: Jamba-1.5 (scaled to 12B/98B)
- Related: [[sources/olmoe|OLMoE]] (open MoE), [[sources/deepseek-v3|DeepSeek-V3]] (different MoE approach)
- Related concepts: [[concepts/state-space-models|State Space Models]], [[concepts/mixture-of-experts|Mixture of Experts]], [[concepts/long-context|Long Context]]
- Key insight: SSMs and Attention are complementary — Mamba handles long-range dependencies efficiently, Attention handles recall-intensive tasks

## Citation
> Lieber et al., "Jamba: A Hybrid Transformer-Mamba Language Model," arXiv:2403.19887, 2024.
