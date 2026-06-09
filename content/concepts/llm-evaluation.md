---
type: concept
tags: [evaluation, benchmark, leaderboard]
---

# LLM Evaluation & Benchmarks

> The standardized tests and methodologies used to measure LLM capabilities — from knowledge (MMLU) to reasoning (MATH, AIME) to coding (HumanEval) to instruction-following (IFEval).

## Overview
Evaluating LLMs is fundamental to the ecosystem — it determines which models get adopted, what research directions are pursued, and how progress is measured. The field has evolved from simple perplexity on held-out data to comprehensive multi-task benchmarks, but persistent challenges remain: benchmark contamination, evaluation sensitivity to prompting, and the gap between benchmark performance and real-world utility.

## Key Benchmarks

### Knowledge & Reasoning
| Benchmark | What It Measures | Tasks | Key Paper |
|---|---|---|---|
| **[[sources/mmlu\|MMLU]]** | Multitask knowledge (57 subjects) | 15,908 MCQ | Hendrycks 2020 |
| **MMLU-Pro** | Harder MMLU (10 options, reasoning-heavy) | — | 2024 |
| **GPQA** | PhD-level science questions | 448 | 2023 |
| **ARC-Challenge** | Grade-school science reasoning | 2,590 | 2018 |

### Mathematics
| Benchmark | What It Measures | Key Paper |
|---|---|---|
| **MATH** | Competition math (7 difficulty levels) | Hendrycks 2021 |
| **MATH-500** | 500-problem MATH subset | Standard eval |
| **GSM8K** | Grade-school math word problems | Cobbe 2021 |
| **AIME 2024** | Math Olympiad (extremely hard) | Competition |

### Code
| Benchmark | What It Measures |
|---|---|
| **HumanEval** | Python function completion (164 problems) |
| **MBPP** | Mostly Basic Python Problems (974) |
| **LiveCodeBench** | Continuously updated code challenges |

### Instruction Following & Chat
| Benchmark | What It Measures |
|---|---|
| **MT-Bench** | Multi-turn conversation quality (GPT-4 judge) |
| **AlpacaEval 2.0** | Instruction following (GPT-4 win rate vs. ref) |
| **IFEval** | Strict instruction-following rules |
| **Arena-Hard** | Challenging prompts from Chatbot Arena |

### Multimodal
| Benchmark | What It Measures |
|---|---|
| **MMMU** | Multidisciplinary multimodal understanding |
| **DocVQA** | Document question answering |
| **ChartQA** | Chart understanding |
| **Video-MME** | Video understanding |

## The HF Open LLM Leaderboard
The Hugging Face Open LLM Leaderboard became the **primary ranking system** for open models:
- Originally used: MMLU, ARC-C, HellaSwag, TruthfulQA, Winogrande, GSM8K
- Leaderboard v2 upgraded benchmarks as models saturated the originals
- Drove massive community investment in benchmark performance

## Challenges
- **Contamination**: Training data may include benchmark questions
- **Prompt sensitivity**: Small prompt changes can cause large score swings
- **Saturation**: Top models score 90%+ on MMLU — ceiling effects
- **Gaming**: Models can be optimized for benchmarks without real capability improvement
- **Static vs. dynamic**: Fixed benchmarks become stale; living benchmarks (LiveCodeBench, Chatbot Arena) provide ongoing signal

## Key Papers
- [[sources/mmlu|MMLU]] — the universal knowledge benchmark
- [[sources/lets-verify-step-by-step|Let's Verify Step by Step]] — evaluation of reasoning with PRMs

## See Also
- [[concepts/scaling-laws|Scaling Laws]]
- [[concepts/test-time-compute|Test-Time Compute Scaling]]
