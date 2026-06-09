---
type: source
arxiv_id: "2605.04916"
title: "A Foundation Model for Zero-Shot Logical Rule Induction"
authors: ["Yin Jun Phua"]
venue: "arXiv preprint"
year: 2026
date: "2026-05"
org: null
upvotes: 3
tags: [reasoning, logic, foundation-model, zero-shot, interpretability, inductive-logic-programming]
github: "https://github.com/phuayj/neural-rule-inducer"
---

# Neural Rule Inducer: A Foundation Model for Zero-Shot Logical Rule Induction

> A pretrained model for **zero-shot rule induction** that represents literals using domain-agnostic statistical properties (class-conditional rates, entropy, co-occurrence) — generalizing across variable identities without retraining, achieving 74.8% on 14 UCI datasets while producing interpretable DNF rules.

## Key Contributions

1. **Domain-agnostic literal encoding**: Represents literals by 18 statistical features (observation rate, positive/negative class rates, entropy, PMI, co-occurrence) rather than identity — enables zero-shot transfer
2. **Parallel slot-based decoder**: Preserves permutation invariance of logical disjunction (an autoregressive decoder would impose arbitrary clause ordering)
3. **Product T-norm relaxation**: Makes rule execution differentiable for end-to-end training on prediction accuracy alone
4. **Trained on synthetic data, transfers to real-world**: Trained exclusively on random boolean formulas, evaluated zero-shot on 14 UCI datasets
5. **Robust to noise and spurious features**: Accuracy degrades only 5% at 30% label noise (vs 28–30% for RIPPER/DT); handles 32 spurious variables with minimal drop

## Method

### Architecture
```
Input: Boolean feature matrix X ∈ {0,1}^{M×N} + labels Y
  → Statistical Encoder: 18 features per literal (rates, entropy, PMI)
  → Example-Conditioned Encoder: Restores per-example information
  → FiLM conditioning: Differentiates clause slots
  → Parallel Slot Decoder: K clause slots in parallel
  → Neuro-Symbolic Execution: Product T-norm for differentiable DNF
Output: Interpretable DNF rule + predictions
```

### Key Design Choices
| Choice | Why |
|---|---|
| Statistical features | Identity-free → generalizes across domains |
| Parallel slots | Permutation-invariant disjunction |
| Product T-norm | Differentiable rule execution |
| Synthetic training | Unlimited diverse training data |
| FiLM conditioning | Prevents clause collapse |

## Results

### Zero-Shot on UCI Datasets (14 datasets, 5% training data)
- **NRI: 74.8%** average accuracy (zero-shot, no per-dataset training)
- XGBoost: 78.2% (non-interpretable, trained per-dataset)
- RIPPER: 71.3% (interpretable, trained per-dataset)
- Neural DNF (scratch): 68.5% (interpretable, trained per-dataset)

### Robustness
| Noise Level | NRI | RIPPER | Decision Tree |
|---|---|---|---|
| 0% | 92.3% | 98.4% | 100% |
| 10% | 91.8% | 89.7% | 87.2% |
| 20% | 89.5% | 78.4% | 76.8% |
| 30% | 87.4% | 70.3% | 69.9% |

NRI degrades gracefully; symbolic methods collapse under noise.

### Computational Efficiency
- Inference: ~7.5ms constant regardless of example count (32–512)
- Sub-linear scaling with feature count N

## Connections

- [[sources/scalelogic|ScaleLogic]] — Both study logical reasoning; ScaleLogic trains LLMs on logical tasks via RL, NRI induces rules from data via meta-learning
- [[sources/scaling-implicit-deductive-reasoning|Implicit Deductive Reasoning]] — Both study logical reasoning capabilities; complementary approaches (neural rule induction vs implicit deductive reasoning in Transformers)
- [[concepts/chain-of-thought|Chain-of-Thought]] — NRI produces explicit interpretable rules; CoT produces informal reasoning traces
