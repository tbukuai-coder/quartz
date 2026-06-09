---
type: entity
category: model
tags: [foundational, google, nlp]
---

# BERT

> Google's **bidirectional encoder** Transformer — the model that established the pre-train + fine-tune paradigm and launched the modern NLP era.

## Overview
BERT (Bidirectional Encoder Representations from Transformers) was released in 2018 and immediately set new SOTA on 11 NLP tasks. Unlike GPT-style models (decoder-only, left-to-right), BERT uses bidirectional attention via masked language modeling. While newer LLMs have shifted to decoder-only architectures, BERT's influence on the field is immeasurable.

## Models

| Model | Params | Layers | Hidden | Heads |
|---|---|---|---|---|
| BERT-Base | 110M | 12 | 768 | 12 |
| BERT-Large | 340M | 24 | 1024 | 16 |

## Legacy
- Established **pre-train + fine-tune** as the standard paradigm
- Spawned variants: RoBERTa, ALBERT, DeBERTa, DistilBERT, etc.
- Still widely used for classification, NER, and embedding tasks
- The Hugging Face `transformers` library was originally built around BERT

## Related Papers
- [[sources/bert]] — Original BERT paper

## See Also
- [[entities/orgs/google]]
- [[concepts/pre-training]]
- [[concepts/fine-tuning]]
- [[concepts/transformer-architecture]]
