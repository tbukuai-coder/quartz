---
type: source
arxiv_id: "2306.01708"
title: "Resolving Interference When Merging Models"
authors: ["Prateek Yadav", "Derek Tam", "Leshem Choshen", "Colin Raffel", "Mohit Bansal"]
date: 2023-06-02
org: "UNC / University of Toronto"
tags: [model-merging, efficiency, transfer-learning, 2023]
upvotes: 18
---

# TIES-Merging

> Resolves parameter interference when merging fine-tuned models by trimming redundant parameters, electing sign consensus, and merging only aligned parameters — the standard algorithm in mergekit.

## Key Contributions
- **Identified three sources of interference**: (1) redundant delta parameters (most are near-zero), (2) sign conflicts between models, (3) magnitude imbalance
- **TIES-Merging**: Trim, Elect sign, and merge — a 3-step algorithm that outperforms simple averaging and task arithmetic
- **Key insight**: 99% of delta parameters can be trimmed without performance loss — fine-tuning creates sparse, high-magnitude changes

## Method
Given multiple fine-tuned models from the same base:
1. **Trim**: For each model, zero out delta parameters (fine-tuned - base) below a threshold (top-k% by magnitude). Typically keep only top 1-20% of deltas
2. **Elect sign**: For each parameter position, take a majority vote across models to determine the consensus sign. Mask out parameters that disagree with the consensus
3. **Merge**: Average the remaining aligned parameters (same sign as consensus) across models
4. **Apply**: Add merged delta to the base model

## Results
- Outperforms: simple averaging, task arithmetic, Fisher merging on 8-task NLP benchmark
- TIES with 20% density matches or exceeds full task arithmetic
- Works across model families: T5, ViT, CLIP
- Scales to merging 8+ models simultaneously
- Combined with [[sources/dare|DARE]] in practice for best results (DARE_TIES strategy)

## Impact on the Ecosystem
TIES-Merging is the **primary algorithm** in `mergekit`, the standard model merging toolkit:
- Used extensively on HF Hub for creating merged models
- Thousands of TIES-merged models on the Open LLM Leaderboard
- Often combined with [[sources/dare|DARE]] as `dare_ties` strategy

## Connections
- Paired with: [[sources/dare|DARE]] (complementary — DARE prunes, TIES resolves conflicts)
- Related: Task Arithmetic, Fisher Merging (predecessors)
- Concepts: [[concepts/model-merging|Model Merging]]
- Tools: mergekit (HF community tool)

## Citation
> Yadav et al., "Resolving Interference When Merging Models," NeurIPS 2023, arXiv:2306.01708.
