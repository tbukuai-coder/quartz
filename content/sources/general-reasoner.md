---
type: source
arxiv_id: "2505.14652"
title: "General-Reasoner: Advancing LLM Reasoning Across All Domains"
authors: ["Xueguang Ma", "Qian Liu", "Dongfu Jiang", "Ge Zhang", "Zejun Ma", "Wenhu Chen"]
date: 2025-05-20
org: "TIGER-AI Lab / University of Waterloo / Sea AI Lab"
tags: [reasoning, rl, cross-domain, grpo, model-based-verifier, 2025]
upvotes: 24
---

# General-Reasoner: Cross-Domain RL with Model-Based Verification

> Breaks the **math/code monopoly** in RLVR by constructing a **230K-question cross-domain verifiable dataset** (physics, chemistry, finance, electronics, humanities) and training with a **generative model-based answer verifier** that replaces brittle rule-based string matching. Zero RL (no SFT warmup) with diverse-domain data **matches GPT-4o** on multiple benchmarks. 223 GitHub ⭐.

## Key Contributions
- **Cross-domain verifiable dataset**: 230K questions from WebInstruct spanning physics, chemistry, finance, electronics, humanities, social sciences — each with verified short answers for RL
- **Model-based answer verifier**: Trained on Gemini-2.0-Flash solutions, performs CoT-based answer equivalence checking — dramatically reduces false negatives where correct but differently-formatted answers are penalized by rule-based matching
- **Zero RL generalization**: Direct RL from base models (no SFT warmup) with diverse-domain data generalizes to unseen domains at inference time
- **GPT-4o competitive**: General-Reasoner-Qwen3-14B matches or beats GPT-4o on GPQA-Diamond (56.1 vs 50.0) and TheoremQA (54.4 vs 43.6)
- **Full release**: 4 model checkpoints (Qwen2.5-7B/14B, Qwen3-4B/14B) + dataset (TIGER-Lab/WebInstruct-verified)

## Method
### Data Pipeline
WebInstruct (5M) → re-crawl source pages → filter for human-verified answers → Gemini-1.5-Pro extracts verifiable short-answer QA (~1M) → Gemini-2.0-Flash annotates answer type/domain/difficulty → filter math below university level → quality control via 8-candidate sampling (remove all-fail and all-pass) → **230K final dataset**

### Model-Based Verifier
- Fine-tuned to perform **CoT-based answer equivalence** — handles format differences (e.g., "4+8t, 1+2t, 17-t" ≡ "x=4+8t, y=1+2t, z=17-t")
- Much higher agreement with ground truth than rule-based matching (50K sample study)

### Training
- **Zero RL** via GRPO on base models (no SFT): reward = +1 if verified correct (with length penalty), -0.5 if no answer extracted
- Infrastructure: 4 nodes × 8× H100; ~2 days (4B/7B), ~4 days (14B)
- Framework: VERL

## Results
### General-Reasoner-Qwen2.5-7B vs Qwen2.5-7B-Instruct
| Benchmark | Instruct | General-Reasoner |
|---|---|---|
| MMLU-Pro | 57.0 | **58.9** |
| GPQA-Diamond | 33.8 | **38.8** |
| SuperGPQA | 30.7 | **34.2** |
| TheoremQA | 36.6 | **45.3** |

### General-Reasoner-Qwen3-14B vs GPT-4o
| Benchmark | GPT-4o | General-Reasoner |
|---|---|---|
| GPQA-Diamond | 50.0 | **56.1** |
| TheoremQA | 43.6 | **54.4** |

### Math Performance (maintained despite cross-domain focus)
- MATH500: 78.6, GSM8K: 94.2 — strong math performance without math-only training

## Connections
- **Builds on**: [[sources/deepseek-r1|DeepSeek-R1]] / R1-Zero, [[sources/deepseekmath|DeepSeekMath/GRPO]]
- **Related**: [[sources/guru|Guru]] (also cross-domain RL), Nemotron-CrossThink, SimpleRL-Zoo
- **Concepts**: [[concepts/grpo|GRPO]], [[concepts/rlhf|RLHF]], [[concepts/data-mixing|Data Mixing]]
- **Comparison**: [[comparisons/rl-reasoning-methods|RL Reasoning Methods]], [[comparisons/reasoning-models|Reasoning Models]]
- **HF Models**: `TIGER-Lab/General-Reasoner-Qwen2.5-7B`, `TIGER-Lab/General-Reasoner-Qwen3-14B`
- **HF Dataset**: `TIGER-Lab/WebInstruct-verified`
- **GitHub**: https://github.com/TIGER-AI-Lab/General-Reasoner

## Citation
> Ma et al., "General-Reasoner: Advancing LLM Reasoning Across All Domains," arXiv:2505.14652, 2025.
