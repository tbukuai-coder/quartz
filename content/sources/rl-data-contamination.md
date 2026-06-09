---
type: source
arxiv_id: "2507.10532"
title: "Reasoning or Memorization? Unreliable Results of Reinforcement Learning Due to Data Contamination"
authors: ["Mingqi Wu", "Zhihao Zhang", "Qiaole Dong", "Various"]
date: 2025-07-14
org: "Fudan / Various"
tags: [reasoning, rl, evaluation, contamination, 2025]
upvotes: 90
---

# Reasoning or Memorization? RL Data Contamination

> Reveals that many RL reasoning improvements may be illusory — MATH-500, AMC, AIME and other benchmarks are contaminated in Qwen2.5's pretraining data, making RL results unreliable.

## Key Contributions
- **Exposed widespread data contamination** in popular reasoning benchmarks (MATH-500, AMC, AIME) within Qwen2.5 pretraining data
- Showed that **even random/incorrect rewards can appear to improve reasoning** on contaminated benchmarks
- RL improvements on Qwen2.5 are **not reproducible on Llama** (uncontaminated) — suggesting memorization not reasoning
- Proposed **RandomCalculation**: a leakage-free synthetic math benchmark
- Called for **fundamental reassessment** of RL reasoning results published on Qwen2.5

## Key Findings
1. **MATH-500, AMC problems appear verbatim** in Qwen2.5 pretraining data (Common Crawl)
2. **RL with random rewards** improves Qwen2.5 on MATH-500 — impossible if the model were truly learning reasoning
3. Same RL methods on **Llama models show no improvement** with random rewards — confirming contamination
4. Proposed **decontamination protocols** and leakage-free evaluation benchmarks
5. Many published papers claiming RL reasoning breakthroughs may need re-evaluation

## Implications
- Results from 2025 RL reasoning papers evaluated only on Qwen2.5 + MATH/AMC should be treated with caution
- Need for **leakage-free benchmarks** (like RandomCalculation, fresh competition problems)
- RL reasoning research should evaluate on **multiple model families** to confirm genuine improvement

## Connections
- **Challenges**: Many papers covered in [[sources/rl-reasoning-survey|RL Survey]], [[sources/prorl|ProRL]]
- **Related**: [[concepts/llm-evaluation|LLM Evaluation]], [[concepts/grpo|GRPO]]
- **Impacts**: [[comparisons/reasoning-models|Reasoning Models]] comparison validity

## Citation
> Wu et al., "Reasoning or Memorization? Unreliable Results of Reinforcement Learning Due to Data Contamination," arXiv:2507.10532, 2025.
