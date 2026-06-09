---
type: source
arxiv_id: "2507.18013"
title: "Technical Report of TeleChat2, TeleChat2.5 and T1"
authors: ["Zihan Wang", "Xinzhang Liu", "Yitong Yao", "Chao Wang", "Yu Zhao", "Zhihao Yang", "Wenmin Deng", "Kaipeng Jia", "Jiaxin Peng", "Yuyao Huang"]
date: 2025-07-30
org: "China Telecom AI / TeleAI"
tags: [open-models, reasoning, tool-use, code, math, sft, dpo, rl, 2025]
upvotes: 11
---

# Technical Report of TeleChat2, TeleChat2.5 and T1

> China Telecom's model family covering general-purpose (TeleChat2), speed-optimized (TeleChat2.5), and reasoning (T1) variants — trained on 10T tokens with SFT + DPO + RL pipeline, with T1-115B surpassing OpenAI o1-mini on MATH500.

## Key Contributions
- **Three-model family**: TeleChat2 (general), TeleChat2.5 (speed-optimized), T1 (reasoning) — all from same pretraining base
- **10T token pretraining**: High-quality and diverse token corpus with minimal architectural changes
- **Two-stage post-training**: Broad capability construction → in-depth precision optimization
- **T1 reasoning model**: T1-115B achieves 94.0% on MATH500, surpassing o1-mini (90.0%) and matching DeepSeek-R1 at scale
- **Strong tool use**: TeleChat2.5-115B outperforms GPT-4o on MATH500 (87.0 vs 75.0) and BFCL (83.39 vs 78.65)
- **Curriculum learning**: Model-driven difficulty assessment for code training with dynamic curriculum
- **Tool-graph data construction**: Graph-based API dependency sampling for balanced-difficulty tool-use training

## Method

### Architecture
- Standard transformer with minimal changes from predecessor (TeleChat)
- TeleBase2-35B and TeleBase2-115B base models
- Context lengths: 8K, 32K, 128K/256K variants

### Pre-training
- **10 trillion tokens** of high-quality diverse data
- Three stages: initial pretraining → long-context annealing → model averaging
- Custom tokenizer optimized for Chinese and multilingual text

### Post-Training Pipeline
1. **SFT**: Tens of millions of diverse instruction samples (code, math, reasoning)
2. **DPO**: Preference optimization with carefully curated pairs
3. **RL**: Reinforcement learning for reasoning and tool use

### Specialized Training Techniques

**Code Training**:
- Two-stage coarse-to-fine fine-tuning
- Automatic test case generation (10 cases per problem)
- Code execution feedback in secure sandbox
- Curriculum learning: start with easier prompts, progress to harder

**Math & Reasoning**:
- Two-stage: broad synthetic data → high-quality curated dataset
- Triple verification: problem quality, answer consistency, reasoning validation
- Multi-model collaborative verification with manual consensus screening

**Tool Use**:
- Tool-graph structure based on API dependencies
- Graph sampling for balanced difficulty distribution
- Multi-turn tool-calling accuracy verification via dependency relationships

**Instruction Following**:
- Constraint set construction (length, formatting, linguistic norms)
- LLM-based instruction evolution with randomly sampled constraints
- Automated validation scripts for each constraint type

## Results

### Pre-trained Models

| Model | Size | MATH | MMLU | HumanEval | Context |
|---|---|---|---|---|---|
| TeleBase2-35B | 35B | 69.2 | 72.4 | 73.8 | 8K–256K |
| Qwen2.5-32B | 32B | 61.2 | 75.6 | 78.0 | — |
| TeleBase2-115B | 115B | 72.0 | 81.0 | 72.6 | 8K–128K |
| Qwen2.5-72B | 72B | 62.0 | 77.2 | 78.7 | — |

### Post-trained Models (Thinking Mode)

| Model | Size | MATH500 | AlignBench | IFEval | BFCL |
|---|---|---|---|---|---|
| T1-35B | 35B | 90.0 | 7.93 | 78.26 | 80.11 |
| Deepseek-R1-Qwen32B-distill | 32B | 94.3 | 7.42 | 73.33 | 76.14 |
| QWQ-32B | 32B | 96.0 | 7.97 | 80.09 | 83.10 |
| T1-115B | 115B | **94.0** | **8.22** | 80.15 | 83.39 |
| OpenAI o1-mini | Unknown | 90.0 | 7.91 | 79.07 | — |

### Post-trained Models (Non-Thinking Mode)

| Model | Size | MATH500 | AlignBench | IFEval | BFCL |
|---|---|---|---|---|---|
| TeleChat2.5-35B | 35B | 77.0 | 7.74 | 78.52 | 78.28 |
| Qwen2.5-32B | 32B | 82.0 | 7.39 | 79.44 | 82.11 |
| TeleChat2.5-115B | 115B | **87.0** | 7.94 | 80.93 | **83.39** |
| GPT-4o-1120 | Unknown | 75.0 | 7.49 | 80.18 | 78.65 |

GitHub: [Tele-AI/TeleChat2](https://github.com/Tele-AI/TeleChat2) (269 ⭐)

## Connections
- Builds on: [[sources/qwen3|Qwen3]] (competitor with thinking/non-thinking modes), [[sources/llama-3|Llama 3]] (general open model), [[sources/deepseek-r1|DeepSeek-R1]] (reasoning model pioneer)
- Cited by / Influenced: Demonstrates strong Chinese telecom player entering the open model race
- Related concepts: [[concepts/agents|Agents & Tool Use]], [[concepts/chain-of-thought|Chain-of-Thought]], [[concepts/instruction-tuning|Instruction Tuning]]
- Related papers: [[sources/qwen3|Qwen3]] (unified thinking modes), [[sources/llama-4|Llama 4]] (competitor reasoning model)

## Citation
> Wang et al., "Technical Report of TeleChat2, TeleChat2.5 and T1," arXiv:2507.18013, 2025.
