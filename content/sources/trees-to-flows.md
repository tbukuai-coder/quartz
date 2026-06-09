---
type: source
arxiv_id: "2605.00414"
title: "Trees to Flows and Back: Unifying Decision Trees and Diffusion Models"
authors: ["Unknown"]
date: 2026-05-02
org: "Unknown"
tags: [decision-trees, diffusion-models, theory, generative-models, neural-network-distillation, 2026]
upvotes: 1
---

# Trees to Flows and Back: Unifying Decision Trees and Diffusion Models

> A crisp mathematical correspondence unifying hierarchical decision trees and diffusion processes via Global Trajectory Score Matching (GTSM), with practical instantiations in tabular data generation (TreeFlow, 2× speedup) and neural network distillation (DSMTree).

## Key Contributions

- **Mathematical unification**: Establishes correspondence between hierarchical decision trees and diffusion processes in appropriate limiting regimes — two ostensibly disparate model classes (discrete/hierarchical vs. continuous/dynamic)
- **Global Trajectory Score Matching (GTSM)**: Shared optimization principle for which gradient boosting (idealized) is asymptotically optimal
- **TreeFlow**: Competitive generation quality on tabular data with higher fidelity and **2× computational speedup**
- **DSMTree**: Novel distillation method transferring hierarchical decision logic into neural networks, matching teacher performance within **2%** on many benchmarks

## Results

- TreeFlow achieves competitive generation on tabular data with 2× speedup
- DSMTree distills decision tree logic into neural nets within 2% of teacher performance
- Conceptual bridge between classical ML (decision trees) and modern generative modeling (diffusion)

## Connections
- Builds on: [[sources/diffusion-models]], [[concepts/diffusion-models]], [[concepts/transformer-architecture]]
- Related concepts: [[concepts/scaling-laws]], [[concepts/quantization]]
- Related papers: [[sources/sd3]], [[sources/dit]], [[sources/rectified-flow]], [[sources/quartet]]
- Cited by / Influenced: Bridging classical and modern ML, tabular generative modeling, model distillation

## Citation
> "Trees to Flows and Back: Unifying Decision Trees and Diffusion Models," arXiv:2605.00414, 2026.
