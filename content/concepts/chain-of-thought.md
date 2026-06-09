---
type: concept
tags: [reasoning, prompting, inference, foundational]
---

# Chain-of-Thought (CoT)

> Eliciting **step-by-step reasoning** from LLMs by prompting them to "think step by step" before giving a final answer — dramatically improving performance on math, logic, and multi-step reasoning tasks.

## Overview
Chain-of-thought prompting is one of the most impactful discoveries in LLM research. By simply asking models to show their work, accuracy on complex reasoning tasks can improve by 20–50+ percentage points. CoT is the foundation of the entire reasoning models paradigm — from prompting techniques to the extended thinking in DeepSeek-R1 and Qwen3.

## How It Works

### Zero-Shot CoT
Add "Let's think step by step" to any prompt:
```
Q: If a store has 45 apples and sells 3/5 of them, how many remain?
A: Let's think step by step.
   3/5 of 45 = 27 apples sold.
   45 - 27 = 18 apples remain.
   The answer is 18.
```

### Few-Shot CoT
Provide examples with reasoning chains in the prompt.

### Self-Consistency
Sample multiple CoT paths and take the majority answer — more robust than a single CoT, trades compute for accuracy.

## From Prompting to Training

| Era | Approach | Example |
|---|---|---|
| 2022 | CoT prompting | "Let's think step by step" |
| 2023 | Process reward models | [[sources/lets-verify-step-by-step|Let's Verify Step by Step]] |
| 2024 | Test-time compute scaling | [[sources/scaling-test-time-compute|Snell et al.]] |
| 2025 | Trained reasoning models | [[sources/deepseek-r1|DeepSeek-R1]] — emergent CoT from RL |
| 2025 | Unified thinking modes | [[sources/qwen3|Qwen3]] — thinking/non-thinking in one model |

## Impact on Benchmarks
- **GSM8K**: CoT typically adds 20–40% accuracy
- **MATH**: CoT is essential — without it, most models score near zero
- **MMMU**: [[sources/internvl-2-5|InternVL 2.5]] gained 3.7 points from CoT alone
- **AIME**: Reasoning models with extended CoT achieve 50–80%

## Connection to Reasoning Models
- [[sources/deepseek-r1|DeepSeek-R1]]: Pure RL produces emergent CoT
- [[sources/s1|s1]]: SFT on reasoning traces + budget forcing
- [[sources/kimi-k15|Kimi k1.5]]: Long-context RL for deeper reasoning
- [[sources/qwen3|Qwen3]]: Thinking mode produces extended internal CoT

## CoT Variants and Extensions

### Interleaved Reasoning
[[sources/interleaved-reasoning|Xie et al. (2025)]] introduced a paradigm where models interleave thinking and answering segments (think-answer-think-answer...) rather than completing all reasoning before answering. This reduces TTFT by 80% and improves Pass@1 accuracy by 12.5% — showing that models inherently possess the ability to produce intermediate conclusions.

### Grounded Reasoning with Images
[[sources/grit|GRIT (2025)]] extends CoT to multimodal settings by generating reasoning chains that interleave natural language with bounding box coordinates, enabling MLLMs to "think with images."

### Reasoning for Instruction Following
[[sources/raif|RAIF (2025)]] demonstrated that vanilla CoT can actually *harm* performance on complex instruction-following tasks because it produces superficial reasoning that merely paraphrases instructions. RL-based deep reasoning (via GRPO) is needed for true constraint satisfaction.

## Key Papers
- Wei et al., "Chain-of-Thought Prompting Elicits Reasoning in LLMs" (2022)
- [[sources/lets-verify-step-by-step]] — Process supervision of reasoning steps
- [[sources/scaling-test-time-compute]] — Optimal compute allocation for CoT
- [[sources/deepseek-r1]] — Emergent CoT from reinforcement learning
- [[sources/qwen3]] — Unified thinking/non-thinking modes
- [[sources/interleaved-reasoning]] — Interleaving thinking and answering for efficiency
- [[sources/grit]] — Visual reasoning chains with bounding boxes
- [[sources/raif]] — Deep reasoning for complex instruction following

## See Also
- [[concepts/test-time-compute]] — Scaling inference compute via reasoning
- [[concepts/process-reward-models]] — Verifying individual reasoning steps
- [[concepts/grpo]] — RL method that produces CoT reasoning
- [[concepts/agents]] — Agent reasoning with tool use
