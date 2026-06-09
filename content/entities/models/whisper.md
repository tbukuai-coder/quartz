---
type: entity
category: model
tags: [speech, multimodal, openai]
---

# Whisper

> OpenAI's **open speech recognition** model trained on 680K hours of multilingual audio — the most widely used open-source speech model, supporting 99 languages with near-human accuracy.

## Overview
Whisper demonstrated that massive weak supervision (noisy internet transcripts) at scale produces remarkably robust speech recognition without fine-tuning. It's the most downloaded audio model on the Hugging Face Hub and has become the default speech-to-text solution.

## Models
| Model | Params | Relative Speed | English WER |
|---|---|---|---|
| Whisper Tiny | 39M | 32× | ~7.6% |
| Whisper Base | 74M | 16× | ~5.5% |
| Whisper Small | 244M | 6× | ~4.3% |
| Whisper Medium | 769M | 2× | ~3.5% |
| Whisper Large-v3 | 1.5B | 1× | ~3.0% |

## Capabilities
- **Transcription**: English and 98 other languages
- **Translation**: Any language → English
- **Language identification**: Detect spoken language
- **Voice activity detection**: Detect speech segments
- **Timestamp prediction**: Word-level timestamps

## Related Papers
- [[sources/whisper]] — Whisper paper

## See Also
- [[entities/orgs/openai]]
- [[concepts/pre-training]]
