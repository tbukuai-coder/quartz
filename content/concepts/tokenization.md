---
type: concept
tags: [nlp, infrastructure, foundational, tokenization]
---

# Tokenization

> The process of converting raw text into a sequence of discrete **token IDs** that neural networks can process — the critical bridge between human-readable text and model-readable numbers.

## Overview
Tokenization is the first step in every NLP pipeline. Every LLM, embedding model, and text classifier converts input text into token IDs before processing. The tokenizer's vocabulary, algorithm, and design choices profoundly affect model quality, multilinguality, and efficiency. A poor tokenizer wastes context window (too many tokens per word), handles rare languages badly, or fragments meaningful subwords.

## How It Works

### Subword Tokenization
Modern LLMs use **subword tokenization** — splitting text into pieces that are smaller than words but larger than characters. This balances vocabulary size, coverage of rare words, and sequence length:

- **Common words** → single tokens: `"the"` → `[the]`
- **Rare words** → multiple subwords: `"tokenization"` → `[token, ization]`
- **Unknown words** → character-level pieces: `"xyzzy"` → `[x, y, z, zy]`

### Algorithms

| Algorithm | Approach | Direction | Used By |
|---|---|---|---|
| **BPE** (Byte Pair Encoding) | Iteratively merge most frequent character pairs | Bottom-up | [[entities/models/llama\|LLaMA]], GPT, [[entities/models/mistral\|Mistral]] |
| **Unigram LM** | Prune large vocabulary based on likelihood | Top-down | T5, XLNet, ALBERT |
| **WordPiece** | BPE variant using likelihood gain for merges | Bottom-up | [[entities/models/bert-model\|BERT]] |
| **Byte-level BPE** | BPE on raw UTF-8 bytes (no UNK tokens) | Bottom-up | GPT-2, [[entities/models/llama\|Llama 3/4]], [[entities/models/qwen\|Qwen]] |

### Key Design Choices
1. **Vocabulary size**: Larger vocab = shorter sequences but bigger embedding table. Typical: 32K–256K tokens
2. **Pre-tokenization**: Whether to split on whitespace/punctuation before subword splitting (language-dependent)
3. **Byte-level fallback**: Operating on UTF-8 bytes eliminates UNK tokens entirely (Llama 3 uses 128K byte-level BPE)
4. **Special tokens**: BOS, EOS, PAD, UNK, and chat template tokens (e.g., `<|im_start|>`)
5. **Normalization**: Unicode normalization (NFKC), case folding, accent removal

## Implementations

| Library | Language | Key Feature |
|---|---|---|
| [[sources/sentencepiece\|SentencePiece]] | C++ (Python bindings) | Language-independent, trains from raw text, lossless |
| HF Tokenizers | Rust (Python bindings) | Fast, flexible, BPE/WordPiece/Unigram |
| tiktoken | Rust (Python bindings) | OpenAI's BPE implementation, used by GPT/Qwen |

## Vocabulary Size Evolution
| Model | Year | Vocab Size | Algorithm |
|---|---|---|---|
| [[entities/models/bert-model\|BERT]] | 2018 | 30,522 | WordPiece |
| LLaMA 1 | 2023 | 32,000 | SentencePiece BPE |
| [[entities/models/mistral\|Mistral 7B]] | 2023 | 32,000 | SentencePiece BPE |
| [[entities/models/llama\|Llama 3]] | 2024 | 128,256 | Byte-level BPE (tiktoken) |
| [[entities/models/qwen\|Qwen2.5]] | 2024 | 151,936 | Byte-level BPE (tiktoken) |
| [[entities/models/gemma\|Gemma]] | 2024 | 256,128 | SentencePiece |

The trend is toward larger vocabularies and byte-level BPE — better multilingual support and shorter sequences at the cost of larger embedding tables.

## Impact on Model Quality
- **Fertility** (tokens per word): Lower is better — fewer tokens means more content fits in the context window. English averages ~1.3 tokens/word; poorly supported languages can reach 3–5×
- **Multilingual fairness**: Models with English-centric tokenizers require more tokens for non-English text, effectively shrinking their context window. Qwen3's 151K vocab specifically addresses CJK, Arabic, and 119 languages
- **Code handling**: Dedicated code tokens (indentation, common keywords) improve code generation efficiency

## The Rare Token Problem and TIDE

[[sources/tide-token-index|TIDE (2026)]] addresses a fundamental design choice in all modern LLMs: a **token index is looked up once at the input embedding layer and permanently discarded**. This single-injection assumption causes two structural failures:

1. **Rare Token Problem**: Zipf-type vocabulary distribution causes rare-token embeddings to be chronically under-trained due to receiving a fraction of the cumulative gradient signal compared to common tokens
2. **Contextual Collapse**: The model loses token identity information as depth increases, leading to degradation on token-sensitive tasks

TIDE introduces **EmbeddingMemory** — a mechanism that reintroduces token identity at each layer through context-free semantic vectors and depth-conditioned softmax routing. This is particularly relevant for diffusion language models where token identity reconstruction is critical.

## Key Papers
- [[sources/sentencepiece]] — Language-independent subword tokenizer (used by LLaMA, Gemma, T5)
- [[sources/bert]] — WordPiece tokenization
- [[sources/llama-3]] — 128K byte-level BPE vocabulary
- [[sources/tide-token-index]] — TIDE: Every layer knows the token beneath the context

## See Also
- [[concepts/transformer-architecture]] — Tokenizer feeds into the embedding layer
- [[concepts/pre-training]] — Tokenizer is trained before model pre-training
- [[concepts/long-context]] — Tokenizer efficiency determines effective context length
