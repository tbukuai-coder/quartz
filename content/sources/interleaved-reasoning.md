---
type: source
arxiv_id: "2505.19640"
title: "Interleaved Reasoning for Large Language Models via Reinforcement Learning"
authors: ["Roy Xie", "David Qiu", "Deepak Gopinath", "Dong Lin", "Yanchao Sun", "Chong Wang", "Saloni Potdar", "Bhuwan Dhingra"]
date: 2025-05-30
org: "IBM Research"
tags: [reasoning, rl, chain-of-thought, efficiency, grpo, ppo, 2025]
upvotes: 15
---

# Interleaved Reasoning for Large Language Models via Reinforcement Learning

> A reinforcement learning training paradigm that teaches LLMs to interleave thinking and answering for multi-hop questions — achieving 12.5% relative accuracy improvement, 37% shorter reasoning, and 80% TTFT reduction.

## Key Contributions
- **Interleaved reasoning paradigm**: Models alternate between `<think>` reasoning segments and `<answer>` answer segments, rather than completing full CoT before answering
- **Conditional intermediate reward**: A novel reward scheme that provides additional signal for correct intermediate answers, applied only when model shows learning progress
- **Efficiency gains**: 12.5% relative Pass@1 accuracy improvement, reasoning length reduced by 37%, TTFT reduced by over 80%
- **Generalization**: Strong cross-domain generalization to tasks without intermediate supervision (GPQA, MMLU, MATH)
- **Algorithm agnostic**: Works with PPO, GRPO, and REINFORCE++

## Method

### Interleaved Generation
Given a multi-hop problem requiring N steps, the model produces:
```
y = think^(1) ∘ answer^(1) ∘ think^(2) ∘ answer^(2) ∘ ... ∘ answer^(N)
```

Intermediate answers are user-visible partial conclusions that the model generates when confident about a self-contained sub-problem.

### Reward Design
Three reward components:
1. **Format reward**: Checks correct interleaved format (think/answer tags)
2. **Final accuracy reward**: Correctness of final answer
3. **Conditional intermediate reward**: Applied only when three conditions are met:
   - Final answer is correct
   - Output format is valid
   - Model shows improvement in current batch vs previous

The conditional gating prevents the model from optimizing for local correctness at the expense of global solution quality.

### RL Algorithms Tested
- **PPO**: Best stability with critic model
- **GRPO**: Efficient, no critic needed
- **REINFORCE++**: Simplest implementation

All three show consistent improvements with interleaved reasoning.

## Results

| Method | Avg Pass@1↑ | TTFT↓ | Notes |
|---|---|---|---|
| Think-Answer | Baseline | Baseline | Standard sequential CoT |
| Interleave (no IR) | Comparable | 80% reduction | Inherent interleaving ability |
| Interleave + IR | +12.5% | 80% reduction | With conditional rewards |

Key findings:
- Models inherently possess interleaved reasoning ability (rapid format reward plateau)
- 7B models show growing response length; 1.5B models show shorter responses — indicating length is not a reliable performance indicator
- Incorrect think-answer responses are 2× longer than correct ones; interleaved reasoning curtails unproductive exploration
- Generalizes to out-of-domain tasks (GPQA, MMLU, MATH) without training on them

## Datasets Used
- **K&K** — Multi-hop QA (in-domain with intermediate ground truth)
- **Musique** — Multi-hop QA (in-domain)
- **MATH** — Mathematical reasoning (OOD)
- **GPQA** — Graduate-level science (OOD)
- **MMLU** — General knowledge (OOD)

## Connections
- Builds on: [[sources/deepseek-r1|DeepSeek-R1]] (GRPO training), [[sources/chain-of-thought|Chain-of-Thought]] (reasoning paradigm)
- Cited by / Influenced: Addresses the overthinking problem in reasoning models
- Related concepts: [[concepts/chain-of-thought|Chain-of-Thought]], [[concepts/grpo|GRPO]], [[concepts/test-time-compute|Test-Time Compute]]
- Related papers: [[sources/deepconf|DeepConf]] (confidence filtering for efficiency), [[sources/repro|RePro]] (process rewards reduce overthinking)

## Citation
> Xie et al., "Interleaved Reasoning for Large Language Models via Reinforcement Learning," arXiv:2505.19640, 2025.
