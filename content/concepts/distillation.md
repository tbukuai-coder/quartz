---
type: concept
tags: [training, distillation]
---

# Distillation

> Transferring knowledge from a **larger/stronger "teacher" model** to a smaller "student" model — enabling smaller models to achieve capabilities they couldn't learn from raw data alone.

## Overview
Knowledge distillation is a key enabler of accessible AI. Rather than training a small model from scratch to be as good as a large one, you use the large model's outputs as training signal. This is especially powerful for alignment, where the teacher's behavior encodes subtle preferences that are hard to specify manually.

## Forms of Distillation in the LLM Ecosystem

### Data Distillation (dSFT)
- Teacher generates high-quality responses to prompts
- Student fine-tunes on teacher outputs
- Used by: [[sources/zephyr]] (GPT-4 as teacher), Alpaca (ChatGPT as teacher)

### Preference Distillation (dDPO)
- Teacher ranks/scores multiple responses
- Student does DPO on teacher-generated preferences
- Used by: [[sources/zephyr]] (GPT-4 scoring UltraFeedback)

### Reasoning Distillation
- Teacher generates long chain-of-thought reasoning
- Student learns to reproduce the reasoning process
- Used by: [[sources/deepseek-r1]] (distilling R1 reasoning into Qwen/Llama bases)

### Classical Distillation (Logit Matching)
- Student matches the teacher's output distribution (soft labels)
- DistilBERT, TinyLlama, etc.

## Key Insight
Distillation often produces **better results than training the student on the same data the teacher was trained on**, because the teacher's outputs encode learned patterns and preferences that raw data doesn't directly express.

## Key Papers
- [[sources/zephyr]] — dSFT + dDPO (distilled alignment)
- [[sources/deepseek-r1]] — Reasoning distillation
- [[sources/self-instruct]] — Data generation as a form of distillation

## See Also
- [[concepts/instruction-tuning]]
- [[concepts/dpo]]
