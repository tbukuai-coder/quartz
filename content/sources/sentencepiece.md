---
type: source
arxiv_id: "1808.06226"
title: "SentencePiece: A simple and language independent subword tokenizer and detokenizer for Neural Text Processing"
authors: ["Taku Kudo", "John Richardson"]
date: 2018-08-19
org: "Google"
tags: [tokenization, nlp, infrastructure, foundational]
upvotes: 3
---

# SentencePiece: A simple and language independent subword tokenizer and detokenizer for Neural Text Processing

> A language-independent subword tokenizer that trains directly from raw text, enabling end-to-end neural text processing without language-specific preprocessing — used by LLaMA, Gemma, T5, and most major open-source LLMs.

## Key Contributions
- Created a language-independent subword tokenizer/detokenizer that works directly on raw unicode text (no pre-tokenization needed)
- Implemented both BPE and unigram language model segmentation algorithms in a single library
- Introduced **lossless tokenization**: treats whitespace as a regular character (using ▁ meta-symbol), enabling perfect round-trip text↔token conversion
- Provided self-contained models: a single .model file contains vocabulary, merge rules, and normalization — ensuring reproducibility
- Released high-performance C++ implementation with Python bindings under Apache 2.0

## Method
SentencePiece comprises four components:

1. **Normalizer**: Unicode NFKC normalization (customizable via TSV rules)
2. **Trainer**: Trains subword model from raw text using either:
   - **BPE** (Byte Pair Encoding): Bottom-up merging of frequent character pairs
   - **Unigram Language Model**: Top-down pruning from large seed vocabulary based on likelihood
3. **Encoder**: Converts raw text → subword token IDs
4. **Decoder**: Converts subword token IDs → raw text (lossless)

Key design choices:
- **Whitespace as character**: Replaces spaces with ▁ before segmentation, so the tokenizer treats the entire input as a sequence of unicode characters. This eliminates language-dependent word boundary detection.
- **No pre-tokenization**: Unlike BPE (Sennrich et al., 2016) which requires pre-tokenized word sequences, SentencePiece operates on raw sentences. Critical for languages without explicit word boundaries (Japanese, Chinese, Thai).
- **Vocabulary ID management**: Directly maps tokens to integer IDs with special token support (UNK, BOS, EOS, PAD).
- **Subword regularization** (optional): Samples from multiple segmentations during training for robustness.

## Results
On English-Japanese translation (KFTT):
- SentencePiece (BPE, from raw) vs. subword-nmt (BPE, pre-tokenized): Comparable BLEU scores (29.55 vs. 29.49 en→ja)
- Training speed: SentencePiece is faster than subword-nmt on Japanese data (no pre-tokenization overhead)
- Segmentation speed: ~50K sentences/sec (comparable to existing tools)

## Adoption in Major Models
| Model | Tokenizer | Algorithm |
|---|---|---|
| [[entities/models/llama\|LLaMA 1/2]] | SentencePiece | BPE |
| [[entities/models/gemma\|Gemma 1/2/3]] | SentencePiece | BPE/Unigram |
| T5 / mT5 | SentencePiece | Unigram |
| [[entities/models/mistral\|Mistral]] | SentencePiece (via HF tokenizers) | BPE |
| [[entities/models/qwen\|Qwen]] | tiktoken-based (BPE, different impl) | BPE |
| BLOOM | SentencePiece | BPE |
| XLNet | SentencePiece | Unigram |

## Connections
- Builds on: BPE (Sennrich et al., 2016), Unigram LM segmentation (Kudo, 2018)
- Used by: [[sources/llama|LLaMA]], [[sources/llama-2|Llama 2]], [[sources/gemma|Gemma]], [[sources/mistral-7b|Mistral]], T5, BLOOM, XLNet, and most open-source LLMs
- Alternative: HF Tokenizers library (Rust implementation, also supports BPE), tiktoken (OpenAI/Qwen)
- Related concepts: [[concepts/tokenization|Tokenization]], [[concepts/transformer-architecture|Transformer Architecture]]
- Ecosystem: 20K+ GitHub stars, integrated into HF Transformers via `AutoTokenizer`

## Citation
> Kudo and Richardson, "SentencePiece: A simple and language independent subword tokenizer and detokenizer for Neural Text Processing," EMNLP 2018, arXiv:1808.06226, 2018.
