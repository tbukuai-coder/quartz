---
type: source
arxiv_id: "2605.00380"
title: "ResRL: Residual-Based Reinforcement Learning with Verifiable Rewards"
authors: null
venue: "arXiv preprint"
year: 2026
date: "2026-05"
upvotes: 3
tags: [reinforcement-learning, reasoning, grpo, diversity, gradient-decoupling]
github: null
---

# ResRL: Residual-Based Reinforcement Learning with Verifiable Rewards

> ResRL decouples gradient updates on overlapping semantic distributions between positive and negative responses by **projecting negative sample representations onto the orthogonal complement of the positive subspace** — preserving shared valid reasoning while selectively suppressing errors.

## Key Contributions

1. **Theoretical framework**: Links Lazy Likelihood Displacement (LLD) to negative-positive head-gradient interference; decomposes gradient inner product into logit and representation components
2. **Single-forward proxy metric**: Orthogonal-complement energy e(x) serves as monotonic upper bound on representation alignment — guides conservative advantage reweighting
3. **Residual-based reweighting**: Computes residual of negative sample distribution after projecting onto positive subspace; dynamically modulates gradient penalty
4. **Computational efficiency**: Low-rank SVD approximation of positive representation matrix + length-scaled reward safeguard against verbosity
5. **SOTA results**: Best Avg@16 and Pass@128 across 12 benchmarks; +9.4% Avg@16 over NSR on Qwen3-4B math; +9.6% CodeForces rating over NSR

## Method

### The Problem: Gradient Conflict in NSR

Standard GRPO/NSR penalizes negative trajectories, but positive and negative responses share substantial token distributions (syntactic structures, partial reasoning steps). When NSR upweights negative penalties, it **inadvertently decreases likelihood of shared valid tokens**.

**Key insight**: Penalties on negatives should be confined to gradient directions **orthogonal to positive representations**.

### Theoretical Foundation

**Lemma 1 (Gradient decomposition)**: For output head W with logits z = Wx:
$$
\langle \nabla_W \ell_1, \nabla_W \ell_2 \rangle = \langle \delta_1, \delta_2 \rangle \cdot \langle x_1, x_2 \rangle
$$
where δ = ∇_zℓ is the backprop signal and x is the token representation.

**Cross-sign interference** splits into:
- Logit-space term: |⟨δ⁻, δ⁺⟩|
- Representation term: |⟨x⁻, x⁺⟩| ← **this is what ResRL controls**

### ResRL Algorithm

1. **Positive subspace construction**: Stack positive token representations X⁺ ∈ ℝ^{|P|×d}, extract top-k principal directions V_k via SVD
2. **Orthogonal-complement energy**: e(x) = (1/d) ‖(I − P_S)x‖² where P_S = V_k V_k^⊤
3. **Residual reweighting**: Modulate negative sample advantages by e(x) — higher residual = more orthogonal to positive subspace = stronger penalty
4. **Length-scaled reward**: Linear discount beyond 3500 tokens (70% at 4096) to curb verbosity exploitation

### Key Hyperparameters
- **Rank k = 64**: Protection-discrimination tradeoff (larger k = more protection but weaker discrimination)
- **Penultimate hidden layer**: More stable semantic signal than final layer
- **Quantile threshold q = 0.1–0.2**: Stricter thresholds converge faster with higher accuracy

## Results

### Mathematics (Avg@16, Qwen3-4B)

| Method | AIME24 | AIME25 | AMC23 | Avg |
|---|---|---|---|---|
| GRPO | 23.5 | 20.3 | 35.2 | 26.3 |
| FlowRL | 28.8 | 25.1 | 42.0 | 32.0 |
| NSR | 30.2 | 26.8 | 43.5 | 33.5 |
| **ResRL** | **36.8** | **34.1** | **52.0** | **40.9** |

- **+9.4% Avg@16** over NSR on Qwen3-4B
- **+7.0% Pass@128** averaged over AIME24/25/AMC23
- Improvements concentrate on harder subsets (AIME24/25 +27.7% over FlowRL)

### Code (CodeForces, Qwen3-8B)

| Method | Rating | Percentile |
|---|---|---|
| NSR | 1340.9 | 54.2% |
| **ResRL** | **1469.5** | **68.1%** |

- **+9.6% rating**, +13.9% percentile — new SOTA

### Agent Tasks (ALFWorld)

| Method | Success Rate |
|---|---|
| PPO | 78.9% |
| EMPG | 76.3% |
| **ResRL** | **86.7%** |

- **+10.4%** over EMPG, +7.8% over PPO

### Function Calling (BFCL Multi-Turn OA)

| Method | OA | B | MF | MP |
|---|---|---|---|---|
| ResT | 40.13 | 50.50 | 45.00 | 32.00 |
| **ResRL** | **41.25** | **48.50** | **47.00** | **34.00** |

- **+2.8%** over ResT on multi-turn tool-use

### Ablation: Rank Selection

| k | AIME24 | AIME25 | Gradient Stability |
|---|---|---|---|
| 8 | 32.1 | 28.5 | Stable but under-covers |
| **64** | **36.8** | **34.1** | **Most stable + accurate** |
| 128 | 35.2 | 32.8 | Bursty gradients |
| 256 | 33.5 | 30.1 | Oscillatory |

- k=8: under-covers positive semantics → shared-but-negative tokens over-penalized
- k≥128: residual contrast collapses → oscillatory updates
- **k=64 is the sweet spot**

## Connections

- [[sources/nonsense-helps-lope|LoPE (Nonsense Helps)]] — Both fix GRPO pathologies; LoPE addresses zero-advantage, ResRL addresses gradient conflict
- [[sources/balanced-aggregation-grpo|Balanced Aggregation]] — Both improve GRPO training stability; ResRL at representation level, Balanced Aggregation at aggregation level
- [[sources/klear-reasoner|Klear-Reasoner]] — Gradient-preserving clipping; ResRL projects onto orthogonal complement instead
- [[sources/deepseek-r1|DeepSeek-R1]] — Foundation for RLVR paradigm that ResRL improves
- [[concepts/grpo|GRPO]] — Core algorithm; ResRL modifies advantage reweighting within GRPO framework
- [[comparisons/rl-reasoning-methods|RL Reasoning Methods]] — Adds ResRL to the post-R1 algorithm toolkit
