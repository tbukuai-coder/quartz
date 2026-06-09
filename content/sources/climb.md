---
type: source
arxiv_id: "2504.13161"
title: "CLIMB: CLustering-based Iterative Data Mixture Bootstrapping for Language Model Pre-training"
authors: ["Various"]
date: 2025-04-17
org: "Various"
tags: [pre-training, data-curation, data-mixing, 2025]
upvotes: 97
---

# CLIMB

> Automatic data mixture optimization via semantic clustering instead of manual domain labels, outperforming manual domain categorizations.

## Key Contributions
- Proposed CLIMB: automatic data mixture optimization via semantic clustering
- Showed web data lacks inherent domain divisions — traditional categories are suboptimal
- Developed ClimbLab toolkit for data mixture experimentation
- Achieved better downstream performance than manually-curated mixtures
- Iterative: cluster -> train proxy -> evaluate -> re-cluster

## Method
1. Semantic clustering: embed documents, cluster into N groups via k-means
2. Proxy model training on different cluster proportions
3. Evaluate downstream performance per mixture
4. Bootstrap: use signals to refine clusters and proportions
5. Transfer to large-scale training

## Results
- Outperforms manually-curated mixtures at all tested model sizes
- Better than DoReMi, RegMix, other automatic methods
- Discovered clusters don't align with traditional domain labels

## Connections
- Builds on: [[sources/data-mixing-laws|Data Mixing Laws]], [[sources/regmix|RegMix]]
- Related concepts: [[concepts/data-mixing|Data Mixing]], [[concepts/pre-training|Pre-training]]

## Citation
> "CLIMB: CLustering-based Iterative Data Mixture Bootstrapping," arXiv:2504.13161, 2025.
