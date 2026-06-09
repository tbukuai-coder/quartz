---
type: source
arxiv_id: "2605.21467"
title: "DelTA: Discriminative Token Credit Assignment for Reinforcement Learning from Verifiable Rewards"
authors: ["Kaiyi Zhang", "Wei Wu", "Yankai Lin"]
date: 2026-05-22
org: "Renmin University of China"
tags: [rl, reasoning, grpo, token-credit-assignment, 2026]
upvotes: 204
---

# DelTA: Discriminative Token Credit Assignment for Reinforcement Learning from Verifiable Rewards

> Introduces a discriminator view of RLVR updates showing how sequence-level rewards implicitly select tokens, then proposes reweighting token-gradient terms to amplify distinctive directions and suppress shared noise.

## Key Contributions
- Derives a **discriminator view of RLVR**: shows that policy-gradient updates act as implicit linear discriminators over token-gradient vectors — a token's probability increases when its gradient aligns more with the positive-advantage centroid than the negative one
- Identifies the weakness: advantage-weighted centroids summarize within-side structure but don't maximize between-side discrimination (shared patterns dominate)
- Proposes **DelTA**: reweights token-gradient terms using coefficients derived from the contrast between positive- and negative-advantage token-gradient aggregates
- **Self-normalized RLVR surrogate**: critic-free, group-relative method that reshapes the induced discriminator
- Achieves consistent improvements over DAPO/GRPO baselines on math reasoning benchmarks

## Method
Standard RLVR updates (DAPO/GRPO) aggregate token gradients weighted by response-level advantage, forming positive/negative side centroids. These centroids are dominated by shared patterns (formatting, common reasoning steps) rather than discriminative tokens. DelTA estimates per-token coefficients from the contrast between side-wise centroids and uses them to reweight the RLVR objective, amplifying tokens that distinguish correct from incorrect responses.

## Results
- Consistent improvement over DAPO and GRPO baselines across math reasoning benchmarks
- Better token-level credit assignment without requiring a separate critic or process reward model
- Computationally lightweight — only requires computing token-gradient aggregates already available in the standard RLVR loop

## Connections
- Builds on: [[sources/deepseek-r1]], [[concepts/grpo]], [[sources/nonsense-helps-lope]], [[sources/balanced-aggregation-grpo]]
- Related: [[sources/resrl]], [[sources/klear-reasoner]], [[comparisons/rl-reasoning-methods]]
- Extends: DAPO/GRPO with fine-grained token-level discrimination

## Citation
> Zhang et al., "DelTA: Discriminative Token Credit Assignment for Reinforcement Learning from Verifiable Rewards," arXiv:2605.21467, 2026.
