---
type: concept
tags: [alignment, reward-modeling, rlhf, training]
---

# Reward Modeling

> Training a model to **predict human preferences** over LLM outputs — the component that provides the training signal for RLHF, GRPO, and other alignment methods.

## Overview
Reward models (RMs) are the bridge between human values and model behavior. They learn to score LLM outputs on quality, helpfulness, safety, or correctness, then provide the reward signal that RL-based alignment optimizes against.

## Types of Reward Models

| Type | Granularity | Training Signal | Used By |
|---|---|---|---|
| **Outcome RM (ORM)** | Whole response | Human pref or correctness | [[sources/instructgpt|InstructGPT]] |
| **Process RM (PRM)** | Per-step | Step-level correctness | [[sources/lets-verify-step-by-step|Let's Verify Step by Step]] |
| **Rule-based rewards** | Varies | Format + correctness rules | [[sources/deepseek-r1|DeepSeek-R1]], [[sources/qwen3|Qwen3]] |
| **AI feedback (RLAIF)** | Whole response | LLM-as-judge | [[sources/constitutional-ai|Constitutional AI]] |
| **Implicit (DPO)** | Whole response | No separate RM needed | [[sources/dpo|DPO]], [[sources/kto|KTO]] |

## Reward Model vs. No Reward Model

| Approach | RM? | Method | Example |
|---|---|---|---|
| RLHF (PPO) | ✅ | RM scores, PPO optimizes | [[sources/instructgpt|InstructGPT]] |
| GRPO | ✅ | Score group of outputs | [[sources/deepseek-r1|DeepSeek-R1]] |
| DPO | ❌ | Preference pairs, supervised loss | [[sources/dpo|DPO]] |
| KTO | ❌ | Binary good/bad signal | [[sources/kto|KTO]] |
| ORPO | ❌ | Combined SFT + alignment | [[sources/orpo|ORPO]] |

## Rule-Based Rewards
A major trend replacing learned RMs with verifiable rules: math correctness checking, code test execution, format verification. Used by [[sources/deepseek-r1|DeepSeek-R1]] and [[sources/qwen3|Qwen3]].

## Challenges
- **Reward hacking**: Policy exploits RM weaknesses
- **Distribution shift**: RM doesn't generalize to new policy outputs
- **Annotation cost**: Human preference data is expensive

## Key Papers
- [[sources/instructgpt]] — RLHF with trained reward model
- [[sources/lets-verify-step-by-step]] — Process reward models
- [[sources/constitutional-ai]] — AI feedback as reward signal
- [[sources/dpo]] — Eliminating the reward model entirely
- [[sources/deepseek-r1]] — Rule-based rewards for reasoning RL

## See Also
- [[concepts/rlhf]] — RLHF pipeline
- [[concepts/grpo]] — GRPO with group-relative rewards
- [[concepts/dpo]] — Alignment without explicit reward models
- [[concepts/process-reward-models]] — Step-level reward models