---
type: concept
tags: [theory, scaling]
---

# Scaling Laws

> Empirical laws that predict model performance as a function of **compute, data, and parameters** — guiding how to optimally allocate training resources.

## Overview
Scaling laws provide the theoretical foundation for decisions like "how big should my model be?" and "how much data do I need?" They have been instrumental in the design of modern LLMs.

## Key Scaling Laws

### Kaplan et al. (OpenAI, 2020)
- Loss follows a power law in model size, data, and compute: `L(N, D, C) ∝ N^{-α} + D^{-β}`
- Suggested **scaling parameters faster than data** for compute-optimal training
- Heavily influenced GPT-3 design

### Chinchilla (Hoffmann et al., 2022)
- Showed that Kaplan overweighted model size — **data should scale proportionally with parameters**
- Rule of thumb: train on ~20 tokens per parameter for compute-optimal training
- A 70B model trained on 1.4T tokens matches a 280B model on 300B tokens
- Directly influenced [[sources/llama|LLaMA]] design

### Data-Constrained Scaling ([[sources/scaling-data-constrained]])
- What happens when you run out of data?
- Data can be repeated ~4× with diminishing but positive returns
- Compute can partially substitute for data
- Code data provides disproportionate value

### Overtraining
- [[sources/smollm2|SmolLM2]] deliberately **overtrained** (11T tokens for 1.7B params = 6,500:1 ratio)
- Far beyond the Chinchilla-optimal ratio (~20:1)
- Works because inference cost matters more than training efficiency for small models

## Key Insight
The right scaling law depends on your constraint. If compute-limited → Chinchilla. If deploying a small model → overtrain on high-quality data. If data-limited → train a bigger model.

## Key Papers
- [[sources/scaling-data-constrained]] — Data repetition scaling
- [[sources/llama]] — Applied Chinchilla scaling laws
- [[sources/smollm2]] — Overtraining strategy


## Scaling Laws for RL Reasoning Depth

[[sources/scalelogic|ScaleLogic (2026)]] establishes a new scaling dimension: **reasoning depth** in RL post-training.

- Training compute T follows a power law with proof depth D: T ∝ D^γ (R² > 0.99)
- The scaling exponent γ increases monotonically with logical expressiveness (1.04 → 2.60)
- **Implication**: Complex reasoning (with disjunction, quantification) requires super-quadratic compute scaling with depth
- Curriculum-based training provides ~3× efficiency gains
- Power law holds across RL algorithms (DAPO, GRPO, REINFORCE++)

This complements Chinchilla-style parameter/data scaling by adding **reasoning complexity** as an independent scaling axis.

## See Also
- [[concepts/pre-training]]
