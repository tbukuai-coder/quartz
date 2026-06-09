---
type: source
arxiv_id: "2311.12022"
title: "System 2 Attention (is something you might need too)"
authors: ["Jason Weston", "Sainbayar Sukhbaatar"]
date: 2023-11-20
org: "Meta AI"
tags: [reasoning, attention, inference, 2023]
upvotes: 5
---

# System 2 Attention (S2A)

> Proposed **System 2 Attention** — a method where LLMs first **regenerate the input context** to remove irrelevant or biasing information, then attend to this cleaned context to produce better answers. Addresses the problem that standard attention can be distracted by irrelevant context, leading to sycophancy and factual errors.

## Key Contributions
- **Two-step attention**: (1) LLM rewrites context removing irrelevant info → (2) LLM answers based on cleaned context
- **Reduces sycophancy**: Models less likely to agree with user opinions when irrelevant opinion is filtered
- **Improves factuality**: Removing distracting context improves factual accuracy
- **Zero-shot applicable**: Works without training — just a prompting strategy
- **Connects to dual-process theory**: "System 1" = standard fast attention, "System 2" = deliberate re-processing

## Method
```
Input: Context + Question (may contain irrelevant/biasing information)
  → Step 1 (System 2): "Given this context, extract only the relevant parts for answering the question"
    → LLM generates cleaned/focused context
      → Step 2: "Given this focused context, answer the question"
        → Better answer (less distracted, less sycophantic)
```

## Results
- **Sycophancy**: Reduced agreement with irrelevant opinions from ~50% to ~15%
- **Factual QA**: Improved accuracy when context contains distracting information
- **Longer contexts**: More beneficial as context length increases (more noise to filter)

## Significance
S2A represents an early form of **test-time compute** — spending more inference FLOPs to improve quality. This idea was later expanded:
- [[sources/scaling-test-time-compute|Scaling Test-Time Compute]] (2024): Formalized compute-optimal test-time strategies
- [[sources/deepseek-r1|DeepSeek-R1]] (2025): Extended thinking as test-time compute
- [[sources/s1|s1]] (2025): Budget forcing for reasoning

## Connections
- Related: [[concepts/test-time-compute]], [[concepts/chain-of-thought]], [[concepts/self-attention]]
- Org: [[entities/orgs/meta|Meta AI]]

## Citation
> Weston & Sukhbaatar, "System 2 Attention (is something you might need too)," arXiv:2311.12022, 2023.
