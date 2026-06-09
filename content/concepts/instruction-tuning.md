---
type: concept
tags: [training, instruction-tuning]
---

# Instruction Tuning

> Fine-tuning a model on (instruction, response) pairs to teach it to **follow user instructions** — the bridge between a base language model and a useful assistant.

## Overview
Base language models are trained to predict the next token. They're powerful but don't naturally follow instructions — they're more likely to continue a prompt than answer it. Instruction tuning teaches the model the conversational pattern of receiving a request and generating a helpful response.

## Approaches
| Approach | Data Source | Scale | Examples |
|---|---|---|---|
| **Human demonstrations** | Expert annotators write responses | Expensive, high quality | [[sources/instructgpt]] |
| **Self-Instruct** | Model generates own instruction data | Cheap, moderate quality | [[sources/self-instruct]], Alpaca |
| **Distillation (dSFT)** | Stronger model generates responses | Cheap, high quality | [[sources/zephyr]] |
| **FLAN** | Convert existing NLP datasets to instruction format | Large scale, diverse | Google FLAN |
| **Community crowdsourcing** | Volunteer annotators | Variable quality | [[entities/datasets/oasst|OASST]] |

## Data Formats
```json
// Messages format (ChatML) — preferred
{"messages": [{"role": "user", "content": "..."}, {"role": "assistant", "content": "..."}]}

// Prompt-completion format
{"prompt": "...", "completion": "..."}

// Text format (already formatted)
{"text": "<|user|>\n...\n<|assistant|>\n..."}
```

## Key Insight
The quality of instruction data matters much more than quantity. [[sources/llama-2|Llama 2]] used only ~27K high-quality demonstrations for SFT, yet produced excellent results. Conversely, [[sources/smollm2|SmolLM2]] showed that data mixing and quality filtering are the primary drivers of small model performance.

## Key Papers
- [[sources/instructgpt]] — Established SFT as alignment step
- [[sources/self-instruct]] — Bootstrapping instruction data
- [[sources/zephyr]] — Distilled SFT from stronger models

## See Also
- [[concepts/fine-tuning]]
- [[concepts/rlhf]]
- [[concepts/distillation]]
