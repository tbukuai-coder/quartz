---
type: comparison
tags: [alignment, synthesis]
---

# Comparison: Alignment Methods — RLHF vs DPO vs GRPO

> How the three dominant alignment methods compare in theory, practice, and results.

## Overview

The alignment problem: **how do you make a language model do what users want?** Three major approaches have emerged, each simplifying the previous:

```
RLHF (2022) → DPO (2023) → GRPO (2024)
Complex RL     No reward model   No critic model
```

## Method Comparison

| Aspect | RLHF (PPO) | DPO | GRPO |
|---|---|---|---|
| **Paper** | [[sources/instructgpt]] | [[sources/dpo]] | [[sources/deepseekmath]] |
| **Year** | 2022 | 2023 | 2024 |
| **Reward Model** | ✅ Required | ❌ Not needed | ✅ or rule-based |
| **Critic/Value Model** | ✅ Required | ❌ Not needed | ❌ Not needed |
| **RL Loop** | ✅ PPO with sampling | ❌ Supervised loss | ✅ PPO-style, group baseline |
| **Data Format** | Prompts + reward model | (prompt, chosen, rejected) triples | Prompts + reward signal |
| **Models in Memory** | 4 (policy, ref, reward, value) | 2 (policy, reference) | 3 (policy, ref, reward) |
| **Training Stability** | Low (sensitive to hyperparams) | High | Medium-High |
| **Compute Cost** | Highest | Lowest | Medium |
| **Best For** | Maximum control | Simple alignment | Reasoning, verifiable tasks |

## When to Use What

### Use RLHF (PPO) when:
- You have a high-quality reward model
- You need maximum control over the optimization
- You're building at large scale with dedicated infrastructure
- Example: [[sources/llama-2]] (Meta's alignment pipeline)

### Use DPO when:
- You have preference data (chosen/rejected pairs)
- You want simple, stable training
- You're working with limited compute
- You want to quickly align a base model
- Example: [[sources/zephyr]] (chat model alignment), [[sources/mixtral]] (Mixtral Instruct)

### Use GRPO when:
- You have **verifiable rewards** (math correctness, code tests, factual accuracy)
- You want RL-based optimization without a critic model
- You're training reasoning capabilities
- Example: [[sources/deepseekmath]] (math reasoning), [[sources/deepseek-r1]] (general reasoning)

## The Evolution of Feedback Sources

| Era | Feedback Source | Method | Papers |
|---|---|---|---|
| 2022 | Human annotators | RLHF | [[sources/instructgpt]] |
| 2022 | AI self-critique + principles | RLAIF (CAI) | [[sources/constitutional-ai]] |
| 2023 | AI-generated preferences | dDPO | [[sources/zephyr]] |
| 2024 | Rule-based rewards (correctness) | GRPO | [[sources/deepseekmath]] |
| 2025 | Pure RL (no SFT warmup) | GRPO | [[sources/deepseek-r1]] |

**Trend**: The field has moved from expensive human feedback toward cheaper AI feedback and verifiable rewards — making alignment more accessible and scalable.

## Key Insight
There isn't one "best" method. The choice depends on:
1. **What reward signal you have**: Human preferences → DPO. Verifiable correctness → GRPO. Complex quality → RLHF.
2. **Your compute budget**: DPO is cheapest. RLHF is most expensive.
3. **Your stability requirements**: DPO is most stable. RLHF requires careful tuning.

## See Also
- [[concepts/rlhf]]
- [[concepts/dpo]]
- [[concepts/grpo]]
- [[concepts/constitutional-ai]]
