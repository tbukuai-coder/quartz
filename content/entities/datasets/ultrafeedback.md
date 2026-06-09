---
type: entity
category: dataset
tags: [dpo, alignment, preference, synthetic]
---

# UltraFeedback

> A large-scale AI preference dataset where GPT-4 scores model responses — used for DPO alignment in [[entities/models/zephyr|Zephyr]] and many open-source alignment pipelines.

## Overview
UltraFeedback addresses the bottleneck of human preference annotation by using GPT-4 as the annotator. For each prompt, multiple models generate responses, and GPT-4 rates them on instruction-following, truthfulness, honesty, and helpfulness.

## Key Details
- **Size**: ~64K prompts with multiple rated completions
- **Annotator**: GPT-4 (AI feedback, not human)
- **Format**: Prompt + multiple completions + scores → converted to chosen/rejected pairs for DPO
- **Dimensions scored**: Instruction-following, truthfulness, honesty, helpfulness
- **HF Hub**: [openbmb/UltraFeedback](https://huggingface.co/datasets/openbmb/UltraFeedback)
- **Binarized version**: Used by Zephyr for dDPO

## Used By
- [[sources/zephyr]] — dDPO preference training
- Widely used in the open-source alignment community

## See Also
- [[entities/datasets/ultrachat]]
- [[concepts/dpo]]
- [[concepts/constitutional-ai]] (related: AI-generated feedback)
