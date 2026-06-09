---
type: source
arxiv_id: "2402.03300"
title: "DeepSeekMath: Pushing the Limits of Mathematical Reasoning in Open Language Models"
authors: ["Zhihong Shao", "Peiyi Wang", "Qihao Zhu", "et al."]
date: 2024-02-05
org: "DeepSeek"
tags: [alignment, grpo, math, 2024]
upvotes: 145
---

# DeepSeekMath: Pushing the Limits of Mathematical Reasoning (GRPO)

> Introduced **Group Relative Policy Optimization (GRPO)** — a variant of PPO that eliminates the need for a critic model by using group-relative rewards — and achieved 51.7% on MATH benchmark with a 7B model.

## Key Contributions
- Introduced **GRPO (Group Relative Policy Optimization)** — a simpler, more memory-efficient alternative to PPO
- Achieved **51.7% on MATH** benchmark without external tools (approaching Gemini-Ultra's 53.2%)
- Built a **data selection pipeline** that mined 120B high-quality math tokens from Common Crawl
- Showed that **continued pre-training** on domain-specific data significantly boosts reasoning
- Demonstrated that RL methods (GRPO) outperform rejection sampling and SFT alone for mathematical reasoning

## Method
### Data Pipeline
- Mine mathematical web pages from Common Crawl using a fastText classifier
- Iteratively refine the classifier to improve recall
- Collect 120B math-related tokens (35.5M web pages)

### GRPO
Standard PPO requires a **critic/value model** (often as large as the policy). GRPO eliminates this:

1. For each prompt, sample **G outputs** from the old policy
2. Score each output with a **reward model** (or ground-truth verifier)
3. Compute **group-relative advantages**: `Â_i = (r_i - mean(r)) / std(r)`
4. Optimize policy with PPO-style clipped objective using these advantages

No value function needed → ~50% memory savings over PPO.

### Training Pipeline
1. Continue pre-training DeepSeek-Coder-Base-v1.5 7B on 120B math tokens
2. SFT on curated math instruction data
3. GRPO with outcome-based reward (correctness of final answer)

## Results
- **MATH**: 51.7% (7B model, no tools) — close to Gemini-Ultra (53.2%)
- **GSM8K**: 88.2%
- GRPO outperforms PPO, DPO, and rejection sampling on mathematical reasoning

## Connections
- **Builds on**: [[sources/instructgpt]] (PPO), [[sources/dpo]] (preference optimization landscape)
- **Extended by**: [[sources/deepseek-r1]] (GRPO at scale for reasoning)
- **Key concepts**: [[concepts/grpo]], [[concepts/rlhf]], [[concepts/scaling-laws]]
- **Models**: [[entities/models/deepseek]]
- **Organizations**: [[entities/orgs/deepseek]]
- **GitHub**: [deepseek-ai/deepseek-math](https://github.com/deepseek-ai/deepseek-math) (3.2K ⭐)

## Citation
> Shao et al., "DeepSeekMath: Pushing the Limits of Mathematical Reasoning in Open Language Models," arXiv:2402.03300, 2024.
> https://huggingface.co/papers/2402.03300
