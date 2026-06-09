---
type: source
arxiv_id: "2409.12186"
title: "Qwen2.5-Coder Technical Report"
authors: ["Qwen Team"]
date: 2024-09-18
org: "Alibaba / Qwen"
tags: [code, open-models, pre-training, 2024]
upvotes: 154
---

# Qwen2.5-Coder

> Alibaba's code-specialized LLM family — **six sizes from 0.5B to 32B** — trained on **5.5 trillion tokens** including source code, text-code grounding, synthetic data, and math. Achieves **SOTA across 10+ code benchmarks** at each size class, outperforming larger models including StarCoder2 and CodeLlama. 154 upvotes.

## Key Contributions
- **Full size range**: 0.5B, 1.5B, 3B, 7B, 14B, 32B — covering edge to cloud deployment
- **5.5T tokens**: Massive code-focused pretraining dataset with 5 data types
- **Three-stage training**: File-level → repo-level → instruction tuning
- **SOTA at every scale**: Each size class outperforms comparable models on code generation, completion, reasoning, and repair
- **Retained general capabilities**: Strong math and NLU alongside code

## Training Data: Qwen2.5-Coder-Data
Five key data types:
1. **Source Code Data**: GitHub code across 92 programming languages with quality filtering
2. **Text-Code Grounding Data**: Code-comment pairs, documentation, tutorials
3. **Synthetic Data**: LLM-generated code problems, solutions, explanations
4. **Math Data**: Mathematical content to strengthen reasoning
5. **Text Data**: General text to preserve NLU capabilities

## Three-Stage Training
1. **File-level pretraining**: Standard next-token prediction on individual files with FIM
2. **Repo-level pretraining**: Files grouped by repository for cross-file understanding
3. **Instruction tuning**: Coarse-to-fine SFT with rejection sampling

## Results
### Code Generation (HumanEval, pass@1)
| Model | Params | HumanEval | MBPP (3-shot) |
|---|---|---|---|
| **Qwen2.5-Coder-32B** | **32B** | **92.7%** | **90.2%** |
| **Qwen2.5-Coder-7B** | **7B** | **88.4%** | **83.5%** |
| DS-Coder-V2-Instruct | 236B | 90.2% | 89.4% |
| GPT-4o | — | 90.2% | — |
| StarCoder2-15B-Instruct | 15B | 73.2% | — |

### Scaling Insight
The paper demonstrates that **scaling data quality and quantity** matters more than model size for code — Qwen2.5-Coder-7B outperforms many 30B+ models.

## Connections
- Builds on: [[sources/qwen25|Qwen2.5]] (base architecture)
- Competes with: [[sources/starcoder-2|StarCoder 2]], [[sources/code-llama|Code Llama]]
- Models: [[entities/models/qwen]]
- Org: [[entities/orgs/alibaba]]

## Citation
> Qwen Team, "Qwen2.5-Coder Technical Report," arXiv:2409.12186, 2024.
