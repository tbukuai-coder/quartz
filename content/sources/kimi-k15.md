---
type: source
arxiv_id: "2501.12599"
title: "Kimi k1.5: Scaling Reinforcement Learning with LLMs"
authors: ["Kimi Team", "Moonshot AI"]
date: 2025-01-21
org: "Moonshot AI"
tags: [reasoning, alignment, rlhf, multimodal, 2025]
upvotes: 129
---

# Kimi k1.5: Scaling Reinforcement Learning with LLMs

> The first detailed public report on **scaling RL for long chain-of-thought reasoning** in a multimodal LLM, demonstrating that a **simple RL framework** (without Monte Carlo tree search, value functions, or process reward models) can achieve **o1-level performance** through long-context scaling and improved policy optimization.

## Key Contributions
- Achieves **o1-level reasoning** with a surprisingly simple approach: long-context RL + improved policy optimization (no MCTS, no value model, no PRM)
- **Long context scaling**: Training with 128K context during RL is crucial — reasoning performance scales with context length
- **Long2Short transfer**: Methods to distill long-CoT reasoning capabilities into efficient short-CoT models, yielding SOTA short-CoT results
- **Multimodal reasoning**: Joint text + vision RL training, achieving strong results on visual reasoning benchmarks
- Key insight: **context length scaling is a new axis** for improving reasoning, complementary to parameter scaling

## Method
### RL Training Pipeline
1. **Pretraining**: Standard multimodal LLM pretraining (text, images, video)
2. **Vanilla SFT**: Standard instruction tuning
3. **Long-CoT SFT warmup**: Small, high-quality dataset of verified long chain-of-thought solutions (similar to DeepSeek-R1's cold start)
4. **Reinforcement Learning**: Online RL with rule-based and model-based rewards

### RL Details
- **Policy optimization**: Improved variant of online policy gradient (not GRPO specifically — their own formulation)
- **Reward signals**:
  - Rule-based: Exact-match correctness for math/code
  - Model-based: Reward model for open-ended tasks
- **Long context**: 128K tokens during RL — model learns to "think longer" on harder problems
- **Curriculum**: Problems sampled by difficulty, ensuring model operates near its capability frontier
- **No MCTS, no value function, no PRM**: Deliberately simple framework, showing these aren't necessary

### Prompt Curation
- Quality and diversity of RL prompts are critical
- Iterative refinement: remove too-easy and too-hard problems
- Balance across math, code, science, logic domains
- Both text and image-based problems included

### Long2Short Transfer
Four methods to compress long-CoT into short-CoT:
1. **Model merging**: Interpolate long-CoT and short-CoT model weights
2. **Shortest rejection sampling**: From long-CoT model, keep only shortest correct solutions for SFT
3. **DPO**: Use short correct solutions as "chosen" and long incorrect ones as "rejected"
4. **Long2short RL**: RL with reward bonus for shorter correct solutions

### Long Context Scaling
- Key finding: both training accuracy and response length scale with RL iterations
- Model naturally learns to use more tokens on harder problems
- 128K context during RL significantly outperforms shorter context limits
- This is a **new scaling axis**: context length at test time improves reasoning, similar to how parameter count improves pretraining

## Results
### Long-CoT (Thinking Mode)
| Benchmark | Kimi k1.5 | OpenAI o1 | DeepSeek-R1 |
|---|---|---|---|
| AIME 2024 | 77.5 | 79.2 | 79.8 |
| MATH-500 | 96.2 | 96.4 | 97.3 |
| Codeforces | 94th %ile | — | 96.3rd %ile |
| MathVista | 74.9 | — | — |

### Short-CoT (Non-Thinking Mode)
| Benchmark | Kimi k1.5 (short) | GPT-4o | Claude 3.5 |
|---|---|---|---|
| AIME 2024 | 60.8 | 9.3 | 16.0 |
| MATH-500 | 94.6 | 76.4 | 78.3 |
| LiveCodeBench | 47.3 | 32.8 | 36.3 |

- Short-CoT Kimi k1.5 **outperforms GPT-4o by up to 550%** on reasoning benchmarks
- Long2Short RL is the most effective transfer method

## Connections
- **Builds on**: [[sources/deepseek-r1]] (concurrent work on RL reasoning), [[sources/deepseekmath]] ([[concepts/grpo|GRPO]]-style RL)
- **Related**: [[sources/lets-verify-step-by-step]] (process rewards — which Kimi k1.5 shows are *not* necessary)
- **Key concepts**: [[concepts/rlhf]], [[concepts/scaling-laws]], [[concepts/distillation]]
- **Organizations**: [[entities/orgs/moonshot-ai]]

## Citation
> Kimi Team, "Kimi k1.5: Scaling Reinforcement Learning with LLMs," arXiv:2501.12599, 2025.
> https://huggingface.co/papers/2501.12599
