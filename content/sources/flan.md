---
type: source
arxiv_id: "2210.03629"
title: "Scaling Instruction-Finetuned Language Models"
authors: ["Hyung Won Chung", "Le Hou", "Shayne Longpre", "et al."]
date: 2022-10-20
org: "Google"
tags: [instruction-tuning, scaling, sft, foundational, 2022]
upvotes: 5
---

# Flan-T5 / Flan-PaLM: Scaling Instruction-Finetuned Language Models

> Demonstrated that **instruction finetuning** scales predictably — finetuning PaLM on **1,836 tasks** (Flan collection) yields **Flan-PaLM**, which outperforms PaLM on nearly every benchmark. Released **Flan-T5** models that became the most widely-used instruction-tuned encoder-decoder models.

## Key Contributions
- **Scaling instruction tuning**: Showed benefits of instruction tuning increase with model scale, number of tasks, and chain-of-thought data
- **Flan collection**: 1,836 finetuning tasks in multiple formats (zero-shot, few-shot, chain-of-thought)
- **Flan-PaLM**: Instruction-tuned PaLM-540B — outperforms base PaLM on nearly all benchmarks
- **Flan-T5**: Open instruction-tuned T5 models (80M–11B) — most downloaded encoder-decoder models on HF Hub
- **Chain-of-thought in finetuning**: Including CoT examples during finetuning improves reasoning

## Results
| Model | MMLU | BBH | TyDiQA | MGSM |
|---|---|---|---|---|
| PaLM 540B | 69.3 | 56.5 | 51.5 | 45.4 |
| **Flan-PaLM 540B** | **73.5** | **66.3** | **54.1** | **72.0** |

Instruction tuning improves all downstream tasks, especially reasoning (+10 points on BBH) and multilingual (+27 points on MGSM).

## Impact
- **Flan-T5 on HF Hub**: Among the most downloaded model families (100M+ monthly downloads)
- Established instruction tuning as a mandatory post-training step
- Flan collection used by many subsequent models including [[sources/olmo-2|OLMo 2]] (FLAN in Dolmino Mix)
- Influenced the shift from task-specific fine-tuning to general instruction following

## Connections
- Builds on: T5, PaLM, [[sources/self-instruct]]
- Data used by: [[sources/olmo-2|OLMo 2]] (Dolmino Mix includes decontaminated FLAN)
- Concepts: [[concepts/instruction-tuning]], [[concepts/chain-of-thought]], [[concepts/fine-tuning]]
- Org: [[entities/orgs/google|Google]]

## Citation
> Chung et al., "Scaling Instruction-Finetuned Language Models," JMLR 2024, arXiv:2210.11416.
