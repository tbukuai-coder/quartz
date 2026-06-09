---
type: source
arxiv_id: "2305.06161"
title: "StarCoder: may the source be with you!"
authors: ["Raymond Li", "Loubna Ben Allal", "Yangtian Zi", "et al."]
date: 2023-05-09
org: "BigCode (Hugging Face + ServiceNow)"
tags: [code, open-models, pre-training, responsible-ai, 2023]
upvotes: 33
---

# StarCoder: may the source be with you!

> Introduced **StarCoder** (15.5B params) — the BigCode community's open Code LLM trained on **1 trillion tokens** of permissively licensed code from [[entities/datasets/the-stack|The Stack]]. Outperformed every open Code LLM at release and matched OpenAI's code-cushman-001, with industry-leading responsible AI practices (PII redaction, opt-out, attribution tools).

## Key Contributions
- **15.5B Code LLM**: Trained on 86 programming languages from The Stack v1.2
- **Fill-in-the-Middle (FIM)**: Natively supports code infilling through prefix-suffix-middle training
- **Multi-Query Attention**: Single KV head for efficient inference
- **8K context length**: Longest context among open Code LLMs at the time
- **Comprehensive responsible AI**: PII redaction pipeline, opt-out mechanism, attribution tools (search index + membership checking)
- **Most comprehensive code evaluation**: Benchmarked across many languages, not just Python

## Method
### Architecture
- Decoder-only Transformer, 15.5B parameters
- **Multi-Query Attention (MQA)**: Single shared KV head — faster inference than standard MHA
- **Learned absolute positional embeddings**
- **Fill-in-the-Middle (FIM)**: 50% probability of FIM transformation during training
- Byte-level BPE tokenizer: 49,152 tokens

### Training Data
- **The Stack v1.2**: Permissively licensed code from GitHub (86 languages)
- ~250GB after deduplication
- Additional sources: GitHub issues, Git commits, Jupyter notebooks, Kaggle notebooks
- **Natural language data**: ~20% (issues, markdown, HTML)
- **Decontamination**: Removed HumanEval, MBPP, APPS, GSM8K, DS1000 solutions

### PII Redaction
- Fine-tuned StarEncoder for NER: names, emails, API keys, passwords, IP addresses
- Crowdsourced annotations from 1,399 workers across 35 countries
- Detected PII replaced with realistic-looking substitutes

## Results
### Python (pass@1)
| Model | HumanEval | MBPP |
|---|---|---|
| **StarCoder** | **33.6%** | **52.7%** |
| StarCoderBase | 30.4% | 49.0% |
| code-cushman-001 (12B) | 33.5% | 45.9% |
| CodeGen-16B-Multi | 18.3% | 32.2% |
| LLaMA-33B | 14.0% | — |

StarCoder also excelled on DS-1000 (data science) and multi-language benchmarks.

## Impact
- Widely used as a base model for code fine-tuning: WizardCoder, Phind, Octocoder
- Established responsible AI standards for code datasets (opt-out, PII, attribution)
- BigCode community: 600+ members across 60+ countries, open governance
- StarCoderBase used in BLOOM-style collaborative research

## Connections
- Data: [[entities/datasets/the-stack|The Stack]]
- Extended by: StarCoder2 (2402.19173)
- Models: [[entities/models/starcoder|StarCoder family]]
- Org: [[entities/orgs/huggingface|Hugging Face]]
- Related: [[sources/code-llama|Code Llama]] (competitor from Meta)

## Citation
> Li et al., "StarCoder: may the source be with you!," arXiv:2305.06161, 2023.
