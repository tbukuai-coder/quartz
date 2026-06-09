---
type: source
arxiv_id: "2402.19173"
title: "StarCoder 2 and The Stack v2: The Next Generation"
authors: ["Anton Lozhkov", "Raymond Li", "Loubna Ben Allal", "et al."]
date: 2024-02-29
org: "BigCode (Hugging Face + ServiceNow + Software Heritage)"
tags: [code, open-models, pre-training, 2024]
upvotes: 156
---

# StarCoder 2 and The Stack v2

> The next generation of BigCode's Code LLMs — **StarCoder2-15B** matches or outperforms **Code Llama 33B** (2× larger) while trained on **The Stack v2** from **Software Heritage** (the largest open code archive). 156 upvotes on HF Papers — the most-upvoted open Code LLM paper.

## Key Contributions
- **Three model sizes**: StarCoder2-3B, 7B, and 15B — covering edge to server deployment
- **The Stack v2**: Massively expanded to 619 programming languages from Software Heritage archive (vs. 86 in v1)
- **Repository-context training**: Files from same repository grouped together (vs. random file grouping in v1)
- **Pull request data**: Novel training data source — code reviews with diff hunks and discussions
- **4+ trillion training tokens**: StarCoder2-15B trained on 4.3T tokens (4× more than v1)

## Method
### Architecture
| Model | Params | Layers | Hidden | Heads | KV Heads | Context | Training Tokens |
|---|---|---|---|---|---|---|---|
| StarCoder2-3B | 3B | 30 | 2560 | 32 | 2 (GQA) | 16K | 3.3T |
| StarCoder2-7B | 7B | 32 | 3584 | 28 | 4 (GQA) | 16K | 3.5T |
| StarCoder2-15B | 15B | 40 | 6144 | 48 | 4 (GQA) | 16K | 4.3T |

Key changes from StarCoder v1:
- **RoPE** (replacing learned positional embeddings)
- **Grouped-Query Attention (GQA)** (replacing MQA)
- **16K context** (doubled from 8K)
- **Repository-context** with file-level FIM

### The Stack v2
- Source: **Software Heritage** archive (largest curated collection of source code)
- 619 programming languages, 67.5B+ files
- Additional data: GitHub issues, pull requests, Jupyter/Kaggle notebooks, documentation
- Enhanced deduplication and PII redaction pipeline
- Decontamination against major benchmarks

## Results
| Model | Params | HumanEval | MBPP | Notes |
|---|---|---|---|---|
| **StarCoder2-15B** | **15B** | **46.3%** | **65.4%** | Matches Code Llama 33B |
| Code Llama 34B | 34B | 48.8% | 55.0% | 2× more parameters |
| StarCoder2-7B | 7B | 35.4% | 54.4% | Strong mid-size |
| StarCoder2-3B | 3B | 31.7% | 53.1% | Best at this size |
| DeepSeek-Coder 33B | 33B | 47.6% | 65.6% | Comparable to SC2-15B |

StarCoder2-15B also excels at multi-language code generation, pull request understanding, and repository-level tasks.

## Impact
- StarCoder2 data pipeline adopted by [[sources/smollm2|SmolLM2]] (Stack-Edu: educational code subset)
- Software Heritage partnership: sustainable, legally clear code data source
- Three sizes enable deployment from edge (3B) to cloud (15B)
- Among most downloaded code models on HF Hub

## Connections
- Builds on: [[sources/starcoder|StarCoder v1]], [[entities/datasets/the-stack|The Stack]]
- Models: [[entities/models/starcoder|StarCoder family]]
- Used by: [[sources/smollm2|SmolLM2]] (Stack-Edu derived from SC2 pipeline)
- Org: [[entities/orgs/huggingface|Hugging Face]]

## Citation
> Lozhkov et al., "StarCoder 2 and The Stack v2: The Next Generation," arXiv:2402.19173, 2024.
