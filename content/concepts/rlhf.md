---
type: concept
tags: [alignment, foundational]
---

# RLHF (Reinforcement Learning from Human Feedback)

> The paradigm of aligning language models with human preferences using a three-stage pipeline: **SFT → Reward Model → RL (PPO)** — making models helpful, harmless, and honest.

## Overview
RLHF addresses a fundamental problem: language models trained on internet text learn to predict text, not to be helpful. RLHF adds a feedback loop where human preferences guide the model toward desired behavior. Introduced at scale by [[sources/instructgpt|InstructGPT]], it became the standard alignment method.

## How It Works

### The Three-Stage Pipeline
1. **Supervised Fine-Tuning (SFT)**
   - Collect demonstrations of desired behavior from humans
   - Fine-tune the base model on these demonstrations
   - Creates a model that can follow instructions but isn't optimized for quality

2. **Reward Model Training**
   - Show the SFT model's outputs to humans in pairs
   - Humans rank which output is better
   - Train a reward model to predict human preferences (Bradley-Terry model)

3. **RL Optimization (PPO)**
   - Use the reward model as a scoring function
   - Optimize the SFT model with Proximal Policy Optimization
   - KL penalty prevents the model from diverging too far from the SFT model

### The Alignment Tax
RLHF slightly reduces performance on traditional benchmarks (the "alignment tax") but dramatically improves perceived quality and safety. A 1.3B InstructGPT is preferred over 175B GPT-3.

## Variants & Extensions
| Method | Key Difference | Paper |
|---|---|---|
| **RLHF (PPO)** | Full pipeline with reward model + RL | [[sources/instructgpt]] |
| **DPO** | No reward model; direct policy optimization | [[concepts/dpo]] |
| **GRPO** | No critic model; group-relative advantages | [[concepts/grpo]] |
| **RLAIF** | AI generates preferences instead of humans | [[concepts/constitutional-ai]] |
| **Rejection Sampling** | Generate many, keep the best | [[sources/llama-2]] |
| **KTO** | Works with binary (good/bad) feedback, no pairs needed | Ethayarajh 2024 |

## Key Papers
- [[sources/instructgpt]] — Established the RLHF pipeline
- [[sources/llama-2]] — Detailed open description of RLHF
- [[sources/dpo]] — Simplified alternative to RLHF
- [[sources/deepseek-r1]] — Pure RL for reasoning

## See Also
- [[concepts/dpo]]
- [[concepts/grpo]]
- [[concepts/instruction-tuning]]
- [[concepts/constitutional-ai]]
