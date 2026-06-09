---
type: source
arxiv_id: "2605.14386"
title: "Darwin Family: MRI-Trust-Weighted Evolutionary Merging for Training-Free Scaling of Language-Model Reasoning"
authors: ["Taebong Kim", "Youngsik Hong", "Minsik Kim", "Sunyoung Choi", "Jaewon Jang", "Junghoon Shin", "Minseo Kim"]
date: 2026-05-15
org: "Independent"
tags: [model-merging, reasoning, training-free, evolutionary, scaling, 2026]
upvotes: 60
---

# Darwin Family: MRI-Trust-Weighted Evolutionary Merging for Training-Free Scaling of Language-Model Reasoning

> Training-free evolutionary merging framework that achieves frontier reasoning via gradient-free weight-space recombination, 14-dimensional merge genomes, MRI-Trust Fusion, and cross-architecture breeding between Transformer and Mamba components.

## Key Contributions
- **14-dimensional adaptive merge genome**: enables fine-grained component- and block-level recombination of model weights
- **MRI-Trust Fusion**: adaptively weights model contributions during merging based on a learned trust parameter per layer/component
- **Architecture Mapper**: enables cross-architecture breeding between Transformer-based and Mamba-based components
- **Training-free scaling**: improves reasoning performance without any gradient computation or additional training data
- Demonstrates that frontier-level reasoning can be improved by reorganizing latent capabilities already in existing checkpoints

## Method
Darwin Family treats model merging as an evolutionary optimization problem. Each merge configuration is encoded as a 14-dimensional genome specifying how to combine component weights at the block level. MRI-Trust Fusion computes per-layer trust parameters that weight each parent model's contribution. An Architecture Mapper enables cross-architecture breeding (e.g., combining a Transformer model with a Mamba model by mapping components). The evolutionary loop breeds, evaluates, and selects merge configurations without any gradient computation.

## Results
- Superior reasoning performance over individual parent models and naive merging methods
- Successfully breeds Transformer × Mamba hybrids
- Training-free — no GPU training required, only inference-time evaluation for selection
- Demonstrated on multiple reasoning benchmarks (MATH, GSM8K, competition problems)

## Connections
- Builds on: [[sources/ties-merging]], [[sources/dare]], [[concepts/model-merging]]
- Related: [[sources/reasoning-vectors]], [[sources/nemotron-3-super]], [[concepts/mixture-of-experts]]
- Related concepts: [[concepts/scaling-laws]], [[concepts/state-space-models]], [[comparisons/reasoning-models]]

## Citation
> Kim et al., "Darwin Family: MRI-Trust-Weighted Evolutionary Merging for Training-Free Scaling of Language-Model Reasoning," arXiv:2605.14386, 2026.
