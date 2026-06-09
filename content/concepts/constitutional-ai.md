---
type: concept
tags: [alignment, safety, rlaif]
---

# Constitutional AI / RLAIF

> Aligning models using **written principles** and **AI self-critique** instead of human preference labels — enabling scalable safety training without human annotation of harmful content.

## Overview
Constitutional AI ([[sources/constitutional-ai|Bai et al. 2022]]) introduced two key ideas: (1) have the AI critique and revise its own outputs based on a set of principles, and (2) use AI-generated preference labels instead of human ones (RLAIF). This makes safety training cheaper, faster, and better for labeler wellbeing.

## How It Works
1. **Write a constitution**: ~15 human-readable principles (e.g., "be harmless," "be honest")
2. **Self-critique**: The model critiques its own responses against the constitution
3. **Self-revision**: The model revises its responses to comply
4. **AI preference labeling**: The model compares response pairs and picks the better one
5. **Train**: SFT on revised outputs + RL against AI preference model

## Impact on the Ecosystem
The RLAIF concept enabled:
- [[sources/zephyr|Zephyr]]: GPT-4 provides preference labels (no human annotation)
- [[entities/datasets/ultrafeedback|UltraFeedback]]: AI-scored preference dataset
- Democratization of alignment (no expensive human annotation infrastructure)

## Key Papers
- [[sources/constitutional-ai]] — Constitutional AI paper

## See Also
- [[concepts/rlhf]]
- [[concepts/dpo]]
