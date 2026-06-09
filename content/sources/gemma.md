---
type: source
arxiv_id: "2403.08295"
title: "Gemma: Open Models Based on Gemini Research and Technology"
authors: ["Gemma Team", "Thomas Mesnard", "Cassidy Hardin", "et al."]
date: 2024-03-13
org: "Google DeepMind"
tags: [open-models, pre-training, safety, 2024]
upvotes: 50
---

# Gemma: Open Models Based on Gemini Research and Technology

> Lightweight open models (2B and 7B) built from **Gemini research**, outperforming similarly sized open models on 11/18 benchmarks, with a strong emphasis on responsible development and safety.

## Key Contributions
- Released **2B and 7B** models — both pretrained and instruction-tuned
- Outperforms similarly sized open models on **11 out of 18** text-based tasks
- Built with Gemini technology and training infrastructure but scaled down
- Comprehensive safety evaluation and filtering — emphasis on responsible AI
- Both pretrained and fine-tuned checkpoints released

## Method
- Architecture based on the Transformer decoder (similar to LLaMA-style)
- Trained on a large corpus of web documents, code, and mathematics
- Uses **Multi-Query Attention** for 2B and **Multi-Head Attention** for 7B
- RMSNorm, GeGLU activation, RoPE embeddings
- Instruction-tuned versions use SFT + RLHF
- Extensive safety training and red-teaming

## Models Released
| Model | Params | Context |
|---|---|---|
| Gemma 2B | 2B | 8192 |
| Gemma 7B | 7B | 8192 |
| Gemma 2B IT | 2B | 8192 |
| Gemma 7B IT | 7B | 8192 |

## Connections
- **Builds on**: [[sources/attention-is-all-you-need]] (Transformer), Google's Gemini research
- **Key concepts**: [[concepts/pre-training]], [[concepts/instruction-tuning]], [[concepts/rlhf]]
- **Models**: [[entities/models/gemma]]
- **Organizations**: [[entities/orgs/google]]
- **Succeeded by**: Gemma 2, Gemma 3 (multimodal)

## Citation
> Gemma Team, "Gemma: Open Models Based on Gemini Research and Technology," arXiv:2403.08295, 2024.
> https://huggingface.co/papers/2403.08295
