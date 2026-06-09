---
type: entity
category: model
tags: [alignment, huggingface, distillation]
---

# Zephyr

> Hugging Face's aligned chat model — built by distilling alignment from GPT-4 into Mistral 7B using dSFT + dDPO, with **zero human annotation**.

## Overview
Zephyr demonstrated that competitive chat models can be built entirely with AI feedback. By distilling both instruction-following behavior (dSFT) and preference alignment (dDPO) from GPT-4, Zephyr-7B topped the MT-Bench leaderboard among 7B models and even outperformed Llama 2-Chat 70B.

## Key Details
- **Base model**: [[entities/models/mistral|Mistral 7B]]
- **Alignment**: dSFT (UltraChat) → dDPO (UltraFeedback)
- **MT-Bench**: 7.34 (best 7B at release)
- **No human annotation** — all feedback from GPT-4

## Significance
Zephyr proved the viability of the "distill alignment from a stronger model" approach, which is now widely used. It was released alongside the **Alignment Handbook** — a practical, reproducible guide for model alignment.

## Related Papers
- [[sources/zephyr]] — Zephyr paper

## See Also
- [[entities/orgs/huggingface]]
- [[entities/models/mistral]]
- [[concepts/dpo]]
- [[concepts/distillation]]
