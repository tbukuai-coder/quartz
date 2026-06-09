---
type: source
arxiv_id: "2605.00623"
title: "EnergyFlow: Recovering Hidden Reward in Diffusion-Based Policies"
authors: ["Yanbiao Ji", "Qiuchang Li", "Yuting Hu", "Shaokai Wu", "Wenyuan Xie", "Guodong Zhang", "Qicheng He", "Deyi Ji", "Yue Ding", "Hongtao Lu"]
venue: "arXiv preprint"
year: 2026
date: "2026-05"
org: null
upvotes: 2
tags: [diffusion, inverse-rl, imitation-learning, robotics, energy-based-models]
github: "https://github.com/sotaagi/EnergyFlow"
---

# EnergyFlow: Recovering Hidden Reward in Diffusion-Based Policies

> Unifies generative action modeling with inverse reinforcement learning by parameterizing a **scalar energy function whose gradient is the denoising field** — enabling reward extraction without adversarial training while constraining the field to be conservative for better OOD generalization.

## Key Contributions

1. **Score–reward equivalence**: Under maximum-entropy optimality, the score function learned via denoising score matching recovers the gradient of the expert's soft Q-function — enabling reward extraction from diffusion policies
2. **Conservative field constraint**: Requiring the learned vector field to be the gradient of a scalar potential reduces hypothesis complexity and tightens OOD generalization bounds (proved formally)
3. **Reward extraction without adversarial training**: The energy function directly provides a reward signal for downstream RL, eliminating the need for discriminator-based IRL
4. **Identifiability and robustness**: Recovered rewards are identified up to state-dependent constants; score estimation errors propagate to action preferences with bounded Lipschitz continuity
5. **SOTA imitation + reward signal**: 93.8% average success on RoboMimic (vs 91.2% Diffusion Policy), and extracted reward enables effective SAC training without ground-truth rewards

## Method

### Core Insight
Standard diffusion policies learn ∇_a log p(a|s) for action generation. EnergyFlow shows this score IS the gradient of the expert's soft Q-function:

```
∇_a log p*(a|s) = (1/α) ∇_a Q*(s,a)
```

By parameterizing an explicit energy E_φ(a,s) and using its gradient as the denoising field, we simultaneously get:
- A generative policy (via diffusion sampling)
- A reward signal (via the energy function directly)

### Conservative Field Constraint
- Standard diffusion: learns arbitrary vector field → no guarantee it's a gradient
- EnergyFlow: learns scalar E_φ, takes ∇_a E_φ → guaranteed conservative (curl-free)
- **Theorem 3.6**: Conservative constraint reduces Rademacher complexity, tightens generalization by O(√(d·log(d)))
- **Lemma 3.8**: Conservative fields extrapolate energy landscape shape to unseen regions

### Training
1. Standard denoising score matching loss on expert demonstrations
2. Network outputs scalar energy; gradient computed via autodiff
3. No adversarial discriminator needed

## Results

| Method | RoboMimic Avg | Meta-World Avg | OOD Robustness |
|---|---|---|---|
| Diffusion Policy | 91.2% | 92.2% | Degrades quickly |
| Flow Policy | 89.6% | 91.0% | Moderate |
| **EnergyFlow** | **93.8%** | **93.4%** | **Most robust** |

- Real robot deployment on AGIBOT G1: successful contact-rich manipulation
- Extracted reward enables SAC to reach 85%+ success without ground-truth rewards (vs GAIL: 78%)
- Inference latency comparable to Flow Policy (non-energy methods)

## Connections

- [[sources/marble|MARBLE]] — Both bridge diffusion and RL; MARBLE for multi-reward generation, EnergyFlow for inverse RL from demonstrations
- [[concepts/diffusion-models|Diffusion Models]] — Reveals reward structure hidden in diffusion score functions
- [[concepts/reward-modeling|Reward Modeling]] — Alternative to discriminator-based IRL for reward extraction
- [[sources/learning-while-deploying|Learning while Deploying]] — Both address policy learning in robotics; complementary approaches (online RL vs imitation+IRL)
- [[sources/trust-imagination-wam|When to Trust Imagination]] — Both improve robotic policy quality
