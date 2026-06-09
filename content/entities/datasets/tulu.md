---
type: entity
category: dataset
tags: [alignment, sft, dpo, instruction-tuning, allenai, open-science]
---

# Tülu

> AllenAI's open **adaptation recipe** for post-training LLMs — a curated mixture of instruction-following, chat, and preference data used to transform base models into aligned assistants, released alongside [[entities/models/olmo|OLMo]].

## Overview
Tülu is AllenAI's post-training pipeline for adapting base language models into helpful, harmless assistants. It combines SFT data with DPO data, providing a complete, open, and reproducible alignment recipe.

## Versions

### Tülu v1
- SFT mix: FLAN, OASST, ShareGPT, Code Alpaca, GPT4-Alpaca, Science QA
- Used to create OLMo-7B-Instruct

### Tülu v2
- Expanded SFT mixture + DPO with [[entities/datasets/ultrafeedback|UltraFeedback]]

### Tülu 3
- Used by [[sources/olmoe|OLMoE-1B-7B-Instruct]]
- Incorporates RLVR (Reinforcement Learning with Verifiable Rewards)
- Expanded code, math, and reasoning coverage

## Pipeline
```
Base Model → SFT (Tülu mix) → DPO (UltraFeedback) → (Optional) RLVR → Aligned Model
```

## Key Design Principles
1. **Diverse sources**: Combine many instruction datasets
2. **Quality filtering**: Remove low-quality examples
3. **Balanced mixing**: Proportion code, math, chat, safety data
4. **Full transparency**: All sources, proportions, and code released

## Related Papers
- [[sources/olmo]] — OLMo (uses Tülu)
- [[sources/olmoe]] — OLMoE (uses Tülu 3)

## See Also
- [[entities/orgs/allenai]] — AllenAI (creator)
- [[entities/models/olmo]] — OLMo models aligned with Tülu
- [[entities/datasets/ultrafeedback]] — UltraFeedback (DPO stage)
- [[concepts/instruction-tuning]] — Instruction tuning concept
- [[concepts/dpo]] — DPO alignment method