---
type: source
arxiv_id: "2407.01492"
title: "RegMix: Data Mixture as Regression for Language Model Pre-training"
authors: ["Qian Liu", "Xiaosen Zheng", "Niklas Muennighoff"]
date: 2024-07-01
org: "Sea AI Lab / Various"
tags: [pre-training, data-mixing, scaling-laws, 2024]
upvotes: 40
---

# RegMix

> Frames data mixture optimization as a regression task — train small models on diverse mixtures, fit a regression model, then predict the optimal mixture for large-scale training.

## Key Contributions
- Framed data mixture optimization as a **regression problem**: predict downstream performance from mixture proportions
- Achieved **significant compute savings**: only 0.5% of target training budget needed for mixture search
- Optimized **1B model mixture** that consistently outperforms uniform and heuristic baselines
- Compared against DoReMi, Skill-It, and manual heuristics — RegMix finds better mixtures
- Demonstrated **mixture sensitivity**: small proportion changes cause large performance shifts

## Method
1. **Sample diverse mixtures**: Generate K random data mixture proportions
2. **Train small proxy models**: Train small models (125M–350M) on each mixture
3. **Evaluate**: Measure downstream task performance for each model
4. **Regression**: Fit a simple regression model mapping mixture proportions → performance
5. **Optimize**: Use the regression model to find the optimal mixture proportions
6. **Transfer**: Apply to full-scale training

## Results
- 1B model on optimized mixture outperforms uniform baseline across downstream tasks
- Better than DoReMi, Skill-It on matched compute budgets
- Regression model accurately predicts performance rankings of unseen mixtures
- Works across different model sizes (125M→1B transfer)

## Connections
- **Related to**: [[sources/data-mixing-laws|Data Mixing Laws]] (complementary approach), [[sources/climb|CLIMB]] (clustering alternative)
- **Related concepts**: [[concepts/data-mixing|Data Mixing & Curation]], [[concepts/scaling-laws|Scaling Laws]]
- **Evaluated on**: [[entities/datasets/redpajama|RedPajama]] domains

## Citation
> Liu et al., "RegMix: Data Mixture as Regression for Language Model Pre-training," arXiv:2407.01492, 2024.
