---
type: entity
category: model
tags: [code, open-models, bigcode, huggingface, pre-training]
---

# StarCoder

> The **BigCode** project's family of open Code LLMs — trained exclusively on **permissively licensed code** from [[entities/datasets/the-stack|The Stack]], with full transparency on data, training, and evaluation. StarCoder2-15B matches or outperforms Code Llama 33B while being 2× smaller.

## Overview
StarCoder is the flagship output of the BigCode community, an open-scientific collaboration between Hugging Face and ServiceNow (with 600+ members) focused on the responsible development of Code LLMs. The project distinguishes itself through its commitment to data provenance: all training data comes from permissively licensed repositories with opt-out mechanisms, PII redaction, and attribution tools. StarCoder models have become the backbone of many open code assistants and are widely used as base models for code-focused fine-tuning.

## Model Family

### StarCoder (v1, 2023)
| Model | Params | Training Data | Context | Key Features |
|---|---|---|---|---|
| StarCoderBase | 15.5B | 1T tokens (The Stack v1.2, 86 languages) | 8K | Multi-query attention, FIM |
| StarCoder | 15.5B | StarCoderBase + 35B Python tokens | 8K | Python-specialized fine-tune |

### StarCoder2 (2024)
| Model | Params | Training Data | Context | Key Features |
|---|---|---|---|---|
| StarCoder2-3B | 3B | 3.3T tokens (The Stack v2) | 16K | Efficient small code model |
| StarCoder2-7B | 7B | 3.5T tokens (The Stack v2) | 16K | Mid-size, strong multilingual |
| StarCoder2-15B | 15B | 4.3T tokens (The Stack v2) | 16K | Matches Code Llama 33B |

## Architecture
- **Decoder-only Transformer** with learned absolute positional embeddings (v1) / RoPE (v2)
- **Multi-query attention (MQA)** — single KV head for fast inference
- **Fill-in-the-Middle (FIM)**: Trained with prefix-suffix-middle format for code infilling
- **Byte-level BPE tokenizer**: 49,152 tokens (v1) / 49,152 tokens (v2)
- **Repository-context training** (StarCoder2): Files from the same repository grouped together, improving cross-file understanding

## Training Data
- **The Stack v1.2** (StarCoder): 86 programming languages, ~250GB of permissively licensed code from GitHub
- **The Stack v2** (StarCoder2): 619 programming languages from Software Heritage archive, 67.5B+ files, 900+ GB. Includes GitHub issues, pull requests, Jupyter/Kaggle notebooks, documentation
- **PII redaction**: Names, emails, API keys, IP addresses detected and masked using a fine-tuned encoder model (StarEncoder)
- **Deduplication**: MinHash-based near-duplicate removal
- **Decontamination**: Removed files containing solutions from HumanEval, MBPP, APPS, GSM8K, DS1000

## Benchmarks

### StarCoder (v1) — Python
| Model | HumanEval (pass@1) | MBPP (pass@1) |
|---|---|---|
| StarCoder | 33.6% | 52.7% |
| StarCoderBase | 30.4% | 49.0% |
| CodeGen-16B-Multi | 18.3% | 32.2% |
| code-cushman-001 | 33.5% | 45.9% |

### StarCoder2 vs. Peers
| Model | Params | HumanEval (pass@1) | MBPP (pass@1) |
|---|---|---|---|
| StarCoder2-15B | 15B | 46.3% | 65.4% |
| Code Llama 34B | 34B | 48.8% | 55.0% |
| StarCoder2-7B | 7B | 35.4% | 54.4% |
| StarCoder2-3B | 3B | 31.7% | 53.1% |

StarCoder2-15B is competitive with Code Llama 34B (2× larger) on code generation tasks.

## Responsible AI
- **Opt-out mechanism**: Code authors can remove their data from The Stack
- **Attribution tools**: Membership checking (Bloom filters) and search index for training data
- **Open Responsible AI Model License (OpenRAIL-M)**: Permissive with use restrictions
- **PII pipeline**: Multi-stage detection and anonymization of personal information

## Impact
- Widely used as a base for code fine-tuning (WizardCoder, Phind, etc.)
- StarCoder2 used in SmolLM2 training pipeline for code data
- BigCode community model: 600+ contributors across 60+ countries
- `bigcode/starcoder2-15b` among the most downloaded code models on HF Hub

## Related Papers
- [[sources/starcoder]] — StarCoder v1 paper
- [[sources/starcoder-2]] — StarCoder 2 and The Stack v2
- [[sources/code-llama]] — Code Llama (Meta's code model competitor)

## See Also
- [[entities/orgs/huggingface]] — Hugging Face (BigCode co-lead)
- [[entities/datasets/the-stack]] — The Stack training data
- [[entities/models/smollm]] — SmolLM2 (uses StarCoder2 data pipeline)
- [[concepts/tokenization]] — BPE tokenization
