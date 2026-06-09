---
type: source
arxiv_id: "2310.11511"
title: "Llemma: An Open Language Model For Mathematics"
authors: ["Zhangir Azerbayev", "Hailey Schoelkopf", "Keiran Paster", "et al."]
date: 2023-10-17
org: "EleutherAI / Princeton"
tags: [math, code, open-models, 2023]
upvotes: 25
---

# Llemma: An Open Language Model For Mathematics

> An open **math-specialized LLM** (7B/34B) built by continued pretraining of Code Llama on **Proof-Pile-2** (55B tokens of math papers, code, and web math). Achieves **SOTA on MATH** among open models at release and can use formal proof assistants. The first major demonstration of domain-specific continued pretraining for mathematics.

## Key Contributions
- **Math-specialized LLM**: 7B and 34B models via continued pretraining of Code Llama
- **Proof-Pile-2**: 55B token math dataset (arXiv papers, OpenWebMath, AlgebraicStack)
- **MATH benchmark SOTA**: Best open-weight performance on MATH at release
- **Tool-integrated reasoning**: Can call Python, Wolfram Alpha, and formal theorem provers (Lean, Isabelle)
- **Fully open**: Models, data, and training code released

## Method
- **Base model**: Code Llama 7B/34B (strong math base from code pretraining)
- **Continued pretraining**: 200B tokens on Proof-Pile-2 (no SFT or RLHF — pure pretraining)
- **Proof-Pile-2 composition**: arXiv math papers, OpenWebMath, AlgebraicStack (formal proofs)

## Results
| Model | Params | MATH | GSM8K | OCWCourses |
|---|---|---|---|---|
| **Llemma-34B** | 34B | **51.5%** | **88.0%** | **18.0** |
| Code Llama 34B | 34B | 12.2% | 29.6% | 8.0 |
| Minerva 62B | 62B | 50.3% | 78.5% | 12.0 |

Llemma-34B matches Google's Minerva (62B, proprietary data) while being fully open and nearly half the size.

## Impact
- Demonstrated that **continued pretraining** on domain-specific data dramatically improves specialized capabilities
- Influenced math training strategies in [[sources/smollm2|SmolLM2]] (FineMath), [[sources/phi-4|Phi-4]], [[sources/deepseekmath|DeepSeekMath]]
- Proof-Pile-2 became a key resource for math pretraining research
- Showed code pretraining helps math (Code Llama base > Llama 2 base for math)

## Connections
- Builds on: [[sources/code-llama|Code Llama]], OpenWebMath
- Related: [[sources/deepseekmath|DeepSeekMath]], [[entities/datasets/finemath|FineMath]]
- Org: [[entities/orgs/eleutherai|EleutherAI]]
- Concepts: [[concepts/pre-training]], [[concepts/chain-of-thought]]

## Citation
> Azerbayev et al., "Llemma: An Open Language Model For Mathematics," ICLR 2024, arXiv:2310.11511.
