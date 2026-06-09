---
type: source
arxiv_id: "2508.15260"
title: "Deep Think with Confidence"
authors: ["Meta AI"]
date: 2025-08-20
org: "Meta AI"
tags: [reasoning, efficiency, inference, 2025]
upvotes: 90
---

# DeepConf (Deep Think with Confidence)

> Uses model-internal confidence signals to filter low-quality reasoning traces, achieving high accuracy while dramatically reducing token generation — making reasoning models more efficient at inference time.

## Key Contributions
- Introduced **DeepConf**: framework for using model-internal confidence signals during reasoning
- **Filters low-quality reasoning traces** before committing to an answer — avoiding overthinking
- Achieves **high accuracy with significantly fewer tokens** than standard reasoning approaches
- Works with **Qwen 3** and other reasoning models out-of-the-box
- Provides a practical solution to the **overthinking problem** in reasoning models

## Method
Key insight: During chain-of-thought reasoning, the model's internal confidence (measured via token probabilities or hidden state features) varies across different reasoning traces. DeepConf:

1. **Generate multiple reasoning traces** for a given problem
2. **Measure internal confidence** of each trace using model-internal signals
3. **Filter**: Discard low-confidence traces early, keep high-confidence ones
4. **Select**: Choose the most confident trace as the final answer

This is more efficient than best-of-N sampling because low-quality traces are identified and discarded early, before full generation.

## Results
- **AIME**: Maintains high accuracy while reducing token generation by 30-50%
- **MATH-500**: Near-identical accuracy with significantly fewer total tokens
- Works across model families (Qwen 3, others)
- Confidence signals are reliable predictors of answer correctness

## Connections
- **Related**: [[sources/prorl|ProRL]] (RL for reasoning), [[sources/deepseek-r1|DeepSeek-R1]]
- **Org**: [[entities/orgs/meta|Meta AI]]
- **Applied to**: [[sources/qwen3|Qwen3]] (demonstrated on Qwen 3 models)
- **Related concepts**: [[concepts/test-time-compute|Test-Time Compute Scaling]], [[concepts/chain-of-thought|Chain-of-Thought]], [[concepts/sampling-strategies|Sampling Strategies]]
- **Problem**: [[concepts/speculative-decoding|Speculative Decoding]] (efficiency at inference)

## Citation
> Meta AI, "Deep Think with Confidence," arXiv:2508.15260, 2025.
