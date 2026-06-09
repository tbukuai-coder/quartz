---
type: source
arxiv_id: "2504.21801"
title: "DeepSeek-Prover-V2: Advancing Formal Mathematical Reasoning via Reinforcement Learning for Subgoal Decomposition"
authors: ["DeepSeek-AI"]
date: 2025-04-30
org: "DeepSeek"
tags: [theorem-proving, reasoning, rl, math, 2025]
upvotes: 4
---

# DeepSeek-Prover-V2

> A formal theorem proving system that combines recursive subgoal decomposition with RL, achieving top performance on Lean 4 theorem proving benchmarks including miniF2F and ProofNet.

## Key Contributions
- **Recursive theorem proving pipeline**: Decomposes complex theorems into subgoals, proves each subgoal, then combines
- Integrates **informal reasoning** (natural language chain-of-thought) with **formal verification** (Lean 4 proofs)
- Uses **RL for subgoal decomposition**: the model learns which decompositions lead to successful proofs
- Achieves top performance on **miniF2F and ProofNet** benchmarks
- Built on **DeepSeek-V3** as backbone, demonstrating that general LLMs can be strong theorem provers

## Method
1. **Subgoal decomposition**: Given a theorem, generate a plan breaking it into manageable lemmas
2. **Individual proof generation**: Prove each subgoal in Lean 4
3. **Proof combination**: Assemble subproofs into a complete formal proof
4. **RL optimization**: Train the decomposition strategy using proof success as reward

## Results
- **miniF2F**: New SOTA among open models
- **ProofNet**: Top performance on undergraduate-level theorems
- Significantly improves on DeepSeek-Prover-V1.5

## Connections
- **Builds on**: [[sources/deepseekmath|DeepSeekMath]], [[sources/deepseek-v3|DeepSeek-V3]]
- **Related**: [[sources/deepseekmath-v2|DeepSeekMath-V2]] (self-verifiable reasoning)
- **Part of**: [[entities/models/deepseek|DeepSeek]] family
- **Related concepts**: [[concepts/chain-of-thought|Chain-of-Thought]], [[concepts/process-reward-models|Process Reward Models]]

## Citation
> DeepSeek-AI, "DeepSeek-Prover-V2," arXiv:2504.21801, 2025.
