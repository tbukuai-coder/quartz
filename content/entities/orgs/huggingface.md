---
type: entity
category: org
tags: [huggingface, ecosystem, tools, open-models, data-curation, multimodal]
---

# Hugging Face

> The **central hub** of the open-source ML ecosystem — maintaining the Transformers library, Hub platform, and producing influential models (Zephyr, SmolLM, SmolVLM, Idefics2) and research (FineWeb, data scaling, alignment, VLM design).

## Key Contributions

### Platform & Tools
- **Hugging Face Hub** — the largest open model/dataset repository
- **Transformers** — the standard library for loading and using LLMs
- **TRL** — Transformer Reinforcement Learning library (SFT, DPO, PPO, GRPO trainers)
- **PEFT** — Parameter-Efficient Fine-Tuning library (LoRA, QLoRA, etc.)
- **Datasets** — standardized dataset loading and processing
- **Accelerate** — distributed training made easy
- **Text Generation Inference (TGI)** — optimized LLM serving
- **smolagents** — lightweight agent framework using [[sources/codeact|CodeAct]] paradigm

### Models
- [[entities/models/zephyr|Zephyr]] — aligned chat model via distilled DPO
- [[entities/models/smollm|SmolLM2]] — data-centric small language model
- [[entities/models/starcoder|StarCoder]] — BigCode Code LLMs (co-led with ServiceNow)
- [[entities/models/bloom|BLOOM]] — BigScience 176B multilingual model (co-organized)
- [[sources/smolvlm|SmolVLM]] — compact vision-language models (256M–2.2B)
- [[sources/idefics2|Idefics2]] — 8B VLM with rigorous design ablation

### Data
- [[entities/datasets/fineweb|FineWeb]] — 15T token pretraining dataset (largest open dataset)
- [[entities/datasets/fineweb|FineWeb-Edu]] — 1.3T token educational content subset
- [[entities/datasets/finemath|FineMath]] — 54B token math-focused pretraining dataset
- [[entities/datasets/the-stack|The Stack]] — BigCode permissively licensed code dataset
- **The Cauldron** — 50 VL datasets for instruction tuning (from [[sources/idefics2|Idefics2]])
- **Cosmopedia** — synthetic textbook dataset for pretraining
- **SmolTalk** — alignment dataset using [[sources/magpie|Magpie]] and other techniques

### Research
- [[sources/fineweb]] — FineWeb dataset and data curation methodology
- [[sources/zephyr]] — Distilled alignment methodology
- [[sources/smollm2]] — Data-centric small model training
- [[sources/scaling-data-constrained]] — Data repetition scaling laws
- [[sources/idefics2]] — VLM design principles
- [[sources/smolvlm]] — Compact multimodal models

## Papers in This Wiki
- [[sources/fineweb]]
- [[sources/zephyr]]
- [[sources/smollm2]]
- [[sources/scaling-data-constrained]]
- [[sources/idefics2]]
- [[sources/smolvlm]]

## See Also
- [[entities/models/zephyr]]
- [[entities/models/smollm]]
- [[entities/models/starcoder]]
- [[entities/models/bloom]]
- [[entities/datasets/fineweb]]
- [[entities/datasets/finemath]]
- [[entities/datasets/the-stack]]
- [[concepts/vision-language-models]]
