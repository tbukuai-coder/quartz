---
type: source
arxiv_id: "2405.21060"
title: "Transformers are SSMs: Generalized Models and Efficient Algorithms Through Structured State Space Duality"
authors: ["Tri Dao", "Albert Gu"]
date: 2024-05-31
org: "Together AI / CMU"
tags: [architecture, ssm, attention, foundational, 2024]
upvotes: 68
---

# Mamba-2 / Structured State Space Duality (SSD)

> Proved that **Transformers and SSMs are closely related** through a theoretical framework connecting them via structured semiseparable matrices. This duality led to **Mamba-2** — a 2–8× faster architecture than [[sources/mamba|Mamba]] that is adopted in [[sources/nemotron-h|Nemotron-H]], Falcon-H1, and other hybrid models.

## Key Contributions
- **State Space Duality (SSD)**: Framework showing SSMs and attention are different decompositions of the same underlying structured matrix (semiseparable matrices)
- **Mamba-2**: New SSM architecture leveraging SSD insight — 2–8× faster than Mamba-1 with comparable quality
- **Unified theory**: Transformers = attention on the full matrix; SSMs = recurrence on the same matrix's semiseparable decomposition
- **Hardware-optimized algorithm**: Mamba-2's SSD algorithm leverages matrix multiplication hardware (Tensor Cores) unlike Mamba-1's scan-based approach
- **Hybrid recipes validated**: Confirmed that mixing attention + Mamba-2 layers yields best quality-efficiency tradeoff

## Method
### The Duality
| Perspective | Computation | Cost per Token | Memory |
|---|---|---|---|
| **Attention** (Transformer) | Materialize full N×N matrix | O(N) | O(N) KV cache |
| **Recurrence** (SSM) | Sequential state updates | O(1) | O(1) fixed state |
| **SSD** (Mamba-2) | Block-decomposed semiseparable | O(1) amortized | O(1) fixed state |

The key insight: Both attention and SSMs can be viewed as operations on a structured matrix. Attention materializes it explicitly; SSMs decompose it into a recurrence. SSD provides an efficient middle ground using block decomposition.

### Mamba-2 Architecture
- Replaces Mamba-1's selective scan with SSD algorithm
- Uses multi-head structure (like attention) instead of single-head SSM
- Leverages Tensor Core matrix multiply hardware → much faster on modern GPUs
- Compatible with attention layers in hybrid configurations

## Results
| Model | Params | Training Speed | Perplexity | vs. Mamba-1 |
|---|---|---|---|---|
| Mamba-2 | 2.7B | 2–8× faster | Equivalent | Much faster |
| Mamba-1 | 2.8B | Baseline | Baseline | — |
| Transformer++ | 2.7B | ~1× (similar to M2) | Slightly worse | — |

Mamba-2 matches Transformer quality while retaining SSM's constant-memory inference advantage.

## Impact
- **[[sources/nemotron-h|Nemotron-H]]** (NVIDIA): Uses Mamba-2 layers for 92% of layers
- **Falcon-H1** (TII): Hybrid Mamba-2 + attention architecture
- Validated the hybrid architecture approach: ~8–10% attention layers + 90% Mamba-2 layers
- Established SSD as the standard SSM implementation replacing original Mamba scan

## Connections
- Builds on: [[sources/mamba|Mamba]] (Mamba-1), [[sources/flash-attention|FlashAttention]] (Tri Dao's IO-aware algorithms)
- Extended by: [[sources/nemotron-h|Nemotron-H]], Falcon-H1
- Creator: Tri Dao ([[entities/orgs/together-ai|Together AI]]) + Albert Gu (CMU)
- Concepts: [[concepts/state-space-models|SSMs]], [[concepts/self-attention|Self-Attention]]

## Citation
> Dao & Gu, "Transformers are SSMs: Generalized Models and Efficient Algorithms Through Structured State Space Duality," ICML 2024, arXiv:2405.21060.
