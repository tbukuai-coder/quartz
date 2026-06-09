---
type: source
arxiv_id: "2312.00752"
title: "Mamba: Linear-Time Sequence Modeling with Selective State Spaces"
authors: ["Albert Gu", "Tri Dao"]
date: 2023-12-01
org: "CMU / Princeton"
tags: [architecture, ssm, long-context, efficiency, foundational, 2023]
upvotes: 150
---

# Mamba — Selective State Space Models

> A linear-time alternative to Transformers that achieves state-of-the-art language modeling by making SSM parameters input-dependent (selective), with 5× higher inference throughput and linear scaling to million-length sequences. 150 HF upvotes, 18K+ GitHub stars.

## Key Contributions
- **Selective State Spaces**: Makes SSM parameters (B, C, Δ) functions of the input — enables content-based reasoning that prior SSMs lacked
- **Hardware-aware parallel algorithm**: Avoids materializing the full state in HBM by using a scan in SRAM — makes selective SSMs efficient despite not being convolvable
- **Simplified architecture**: No attention blocks, no MLP blocks — just selective SSM blocks with linear projections. Simpler than Transformers
- **5× inference throughput** over Transformers with linear (not quadratic) scaling in sequence length
- **Mamba-3B outperforms Transformers of same size** and matches Transformers twice its size on language modeling

## Method
1. **State Space Models (SSMs)**: Map inputs to outputs through a hidden state, similar to RNNs but with structured transition matrices. Standard SSMs (S4) use fixed parameters — they can't do content-based selection
2. **Selection mechanism**: Makes B (input projection), C (output projection), and Δ (step size) functions of the input. This lets the model decide what to remember/forget based on content — analogous to gating in LSTMs but with structured linear dynamics
3. **Hardware-aware algorithm**: Since selective SSMs can't use convolutions (parameters are time-varying), Mamba uses a parallel scan algorithm that:
   - Loads SSM states into GPU SRAM (not HBM)
   - Computes the scan entirely in SRAM
   - Never materializes the full O(BLDN) state in HBM
4. **Architecture**: Each Mamba block: Linear projection → Conv1d → Selective SSM → Output projection. No attention, no MLP. Residual connections between blocks. Models from 130M to 2.8B parameters

## Results
- **Language modeling**: Mamba-3B outperforms Transformers of same size on the Pile; matches Transformers twice its size (6.6B)
- **Scaling laws**: Favorable scaling — perplexity improves steadily with model size, matching or exceeding Transformer scaling curves
- **Inference**: 5× higher throughput than Transformers; actual speedup grows with sequence length (linear vs quadratic)
- **Long sequences**: Performance improves up to 1M+ tokens on synthetic tasks
- **Cross-modal**: State-of-the-art on audio (SaShiMi) and genomics (HG38) as well as language
- **Zero-shot evaluation**: Matches or exceeds Pythia, RWKV at equivalent sizes on standard NLP benchmarks

## Models Released
- **Mamba-130M, 370M, 790M, 1.4B, 2.8B** — all open-source
- Adopted in: Jamba (AI21), Zamba (Zyphra), FalconMamba (TII), various hybrid architectures

## Connections
- Challenges: [[concepts/transformer-architecture|Transformer Architecture]], [[concepts/self-attention|Self-Attention]]
- Complementary: [[sources/flash-attention|FlashAttention]] (efficient attention vs. no attention)
- Concept: [[concepts/state-space-models|State Space Models]], [[concepts/transformer-architecture|Transformer Architecture]]
- Related: RWKV (alternative subquadratic architecture), Hyena (gated convolution)
- HF integration: `transformers` library has native Mamba support via `MambaForCausalLM`

## Citation
> Gu & Dao, "Mamba: Linear-Time Sequence Modeling with Selective State Spaces," arXiv:2312.00752, 2023.
