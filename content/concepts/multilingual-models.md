---
type: concept
tags: [nlp, multilingual, pre-training, tokenization]
---

# Multilingual Models

> LLMs designed to understand and generate text in **multiple languages** — from bilingual to 100+ language coverage, with implications for tokenizer design, data balance, and evaluation.

## Multilingual Coverage

| Model | Languages | Vocab Size | Strategy |
|---|---|---|---|
| mBERT | 104 | 110K | Multilingual Wikipedia |
| BLOOM | 46 | 250K | Balanced mix |
| [[entities/models/llama\|Llama 3]] | Primarily English | 128K | Byte-level BPE handles any language |
| [[entities/models/qwen\|Qwen3]] | **119** | 151K | Explicit multilingual curation |
| [[entities/models/gemma\|Gemma 3]] | ~140 | 256K | Largest vocabulary |

## Key Challenges

### Tokenizer Fairness
English-centric tokenizers produce 2–5× more tokens for non-English text, effectively shrinking the context window. Solution: larger vocabularies with non-English tokens ([[concepts/tokenization|Tokenization]]).

### Data Balance
English dominates web crawls (60%+ of Common Crawl). Solutions: upsampling low-resource languages, parallel/translated data, cross-lingual transfer.

### Cross-Lingual Transfer
Models trained on English can answer in French — cross-lingual transfer enables low-resource language capability. Stronger with larger vocabularies and deliberate multilingual pre-training.

## Key Papers
- [[sources/qwen3]] — 119 languages, largest multilingual open LLM
- [[sources/sentencepiece]] — Language-independent tokenizer
- [[sources/e5]] — Multilingual contrastive embeddings

## See Also
- [[concepts/tokenization]] — Tokenizer design for multilingual
- [[concepts/pre-training]] — Multilingual data curation
- [[concepts/embeddings]] — Multilingual text embeddings
- [[concepts/contrastive-learning]] — Cross-lingual representations