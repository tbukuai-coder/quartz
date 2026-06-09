---
type: source
arxiv_id: "2605.06548"
title: "Cola DLM: Continuous Latent Diffusion Language Model"
authors: null
venue: "arXiv preprint"
year: 2026
date: "2026-05"
upvotes: 28
tags: [diffusion, language-models, non-autoregressive, latent-models, text-generation]
github: null
---

# Cola DLM: Continuous Latent Diffusion Language Model

> A hierarchical latent-space diffusion language model that decomposes text generation into **global semantic modeling in continuous latent space** and **local textual realization through conditional decoding** — establishing a new paradigm for language generation with flexible non-autoregressive inductive bias.

## Key Contributions

1. **Hierarchical latent-space language model**: Decomposes text generation into global semantic organization (continuous latent) and local textual realization (conditional decoder) within a unified probabilistic framework
2. **Diffusion-based latent prior transport**: Uses diffusion not for token-level observation recovery, but for latent prior transport — weakening the fixed left-to-right inductive bias
3. **Block-causal DiT prior modeling**: Preserves cross-block causal structure while enabling parallel computation within each block
4. **Theoretical Markov-path analysis**: Clarifies advantages in global semantic modeling, non-autoregressive bias, and interpretability vs autoregressive, discrete diffusion, and continuous diffusion baselines
5. **Extensive empirical validation**: 4 RQs, 8 benchmarks, ~2B matched baselines, scaling curves up to ~2000 EFLOPs
6. **Cross-modal bridge**: Preliminary evidence that the framework naturally extends to continuous modalities like vision

## Method

### Three-Stage Architecture

1. **Text VAE Pretraining** (500M params)
   - Encoder: maps text → continuous latent variables
   - Decoder: reconstructs text conditioned on latent
   - Objective: reconstruction + KL divergence + BERT-style masking loss (prevents encoder collapse)
   - Strictly causal to prevent information leakage

2. **Block-Causal DiT Prior Learning** (1.8B params)
   - Models the latent prior in continuous latent space with Flow Matching
   - Block-causal visibility: bidirectional attention within block, causal across blocks
   - Joint objective: Flow Matching + reference-encoder regularizer (prevents latent drift)

3. **Inference: Prefix Encoding + Block-wise Generation + Conditional Decoding**
   - Encode prefix into clean latent conditions
   - Generate response latent blocks autoregressively in latent space
   - Decode text conditioned on prefix + generated latent blocks

### Key Design Insights

| Aspect | AR Models | Discrete Diffusion | Continuous Diffusion (Plaid) | **Cola DLM** |
|---|---|---|---|---|
| **Generation order** | Fixed left-to-right | Flexible but token-level | Flexible but token-aligned | **Flexible, latent-level** |
| **Inductive bias** | Strong sequential | Moderate | Moderate | **Weakened** |
| **Global semantics** | Emergent from token chain | Limited by discrete states | Not explicitly modeled | **Explicitly modeled** |
| **Latent prior** | None | None | Token-aligned recovery | **Continuous prior transport** |

## Results

### RQ1: Global Semantic Structures Exist in Latent Space
- **Key finding**: Optimal timestep shift (loc) systematically drifts with latent dimension — impossible if latent were purely local/separable
- At d=16: best loc ≈ 1.0; d=64: loc ≈ 1.7; d=128: loc ≈ 2.3
- Trend consistent across LAMBADA, MMLU, SIQA → shared cross-dimensional semantic structures

### RQ2: Optimal Latent Space Design
- **Evolving latent space** > fixed latent space (stable training, better semantic metrics)
- Latent dimension trade-off: larger = better semantic representation but harder prior fitting
- Smoothness matters: strongly correlated with generation quality

### RQ3: Diffusion Process Effectiveness
- Flow Matching > DDPM-style noise prediction for latent-space generation
- Block-causal structure outperforms full bidirectional (preserves cross-block dependencies)

### RQ4: Scaling Performance
- Strictly matched ~2B baselines (AR and LLaDA) across same tokenizer, data, optimization
- Cola DLM shows **favorable scaling curves** up to ~2000 EFLOPs
- Competitive or better on multiple benchmarks despite different inductive bias

### The Likelihood-Generation Gap
- **Critical finding**: Estimated perplexity exhibits substantial mismatch with actual generation quality
- Flow Matching training naturally misaligned with conditional PPL estimation
- Even if prior mean is close to ground truth, PPL may still be poor
- **Implication**: PPL should not be sole evaluation metric for latent diffusion LMs

## Connections

- [[sources/trees-to-flows|Trees to Flows]] — Unifies decision trees and diffusion via GTSM; Cola DLM takes the complementary direction (latent space for language)
- [[sources/latent-diffusion|Latent Diffusion]] — Cola DLM adapts latent diffusion principles to language, with block-causal structure for sequential coherence
- [[sources/dit|DiT]] — Diffusion Transformer backbone for the prior model
- [[sources/continuous-time-distribution-matching|Continuous-Time DMD]] — Continuous-time distillation; Cola DLM uses continuous latent space but discrete block-wise generation
- [[concepts/diffusion-models|Diffusion Models]] — Cola DLM extends diffusion to language via hierarchical latent decomposition
- [[concepts/transformer-architecture|Transformer Architecture]] — Block-causal DiT variant
- [[concepts/rectified-flow|Rectified Flow]] — Flow matching objective for the latent prior
