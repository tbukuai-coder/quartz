---
type: entity
category: dataset
tags: [sft, crowdsourced, chat]
---

# OASST (Open Assistant)

> A crowdsourced, human-generated conversational dataset — used to train [[entities/models/guanaco|Guanaco]] and many early open-source chat models.

## Overview
The Open Assistant (OASST) project collected multi-turn conversations between humans and AI assistants through a volunteer annotation effort. OASST1 contains ~161K messages in 35 languages, with human quality ratings.

## Key Details
- **Size**: ~161K messages across ~66K conversation trees
- **Source**: Crowdsourced (volunteer human annotators)
- **Languages**: 35 languages (primarily English)
- **Quality**: Human-rated on multiple dimensions
- **HF Hub**: [OpenAssistant/oasst1](https://huggingface.co/datasets/OpenAssistant/oasst1)

## Used By
- [[sources/qlora]] — Training data for Guanaco models
- Many early community chat models

## See Also
- [[entities/datasets/ultrachat]]
- [[concepts/instruction-tuning]]
