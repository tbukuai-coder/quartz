---
type: comparison
tags: [reasoning, rl, test-time-compute, synthesis, 2025]
---

# Comparison: Reasoning Models — DeepSeek-R1 vs Kimi k1.5 vs Qwen3 vs s1 vs Open-Reasoner-Zero

> How the five major approaches to building o1-style reasoning LLMs compare in training methodology, architectural choices, and results.

## Overview

The "reasoning model" paradigm emerged in late 2024 with OpenAI's o1, followed by open alternatives using three distinct approaches: **RL-based** (DeepSeek-R1, Kimi k1.5, Qwen3, Open-Reasoner-Zero) and **SFT-based** (s1). All share the core idea of extended chain-of-thought reasoning, but differ in how they elicit it.

```
DeepSeek-R1 (Jan 2025): GRPO + multi-stage pipeline + distillation
Kimi k1.5 (Jan 2025): Simple RL + long context scaling + long2short
s1 (Jan 2025): SFT on 1K examples + budget forcing (simplest approach)
Open-Reasoner-Zero (Mar 2025): PPO > GRPO, 10× more efficient
Qwen3 (May 2025): GRPO + thinking mode fusion + unified deployment
```

## Comparison Table

| Aspect | DeepSeek-R1 | Kimi k1.5 | s1 | Open-Reasoner-Zero | Qwen3 |
|---|---|---|---|---|---|
| **Paper** | [[sources/deepseek-r1]] | [[sources/kimi-k15]] | [[sources/s1]] | [[sources/open-reasoner-zero]] | [[sources/qwen3]] |
| **Date** | Jan 2025 | Jan 2025 | Jan 2025 | Mar 2025 | May 2025 |
| **Approach** | RL (GRPO) | RL (custom) | **SFT** | RL (PPO) | RL (GRPO) |
| **Base Model** | DeepSeek-V3 (671B) | Kimi proprietary | Qwen2.5-32B-Instruct | Qwen2.5-{7B,32B} base | Qwen3 base |
| **Training Data** | RL reward only | RL reward only | **1K examples** | RL reward only | RL reward + cold start |
| **Reward** | Rule-based | Rule + model | None (SFT) | Rule-based | Rule-based |
| **Key Innovation** | R1-Zero (pure RL) | Long context scaling | Budget forcing | PPO > GRPO | Think/no-think fusion |
| **Training Cost** | Very high | High | **26 min on 16×H100** | 1/10 of R1-Zero | High |
| **Open Weights** | ✅ MIT | ❌ Proprietary | ✅ Open | ✅ Open | ✅ Apache 2.0 |

## Key Results

### AIME 2024 (Math Olympiad)
| Model | Score | Method |
|---|---|---|
| [[sources/klear-reasoner\|Klear-Reasoner-8B]] | **90.5** | GPPO (gradient-preserving RL) |
| Qwen3-235B-A22B | 81.5 | RL (GRPO) |
| DeepSeek-R1 | 79.8 | RL (GRPO) |
| Kimi k1.5 | 77.5 | RL (custom) |
| s1-32B (budget forced) | 57% | SFT + budget forcing |
| ORZ-32B | 53.3 | RL (PPO) |

### Training Efficiency
| Model | Training Compute | Result |
|---|---|---|
| **s1** | 26 min on 16×H100 | Beats o1-preview on MATH |
| **ORZ** | 1/10 of R1-Zero steps | Matches R1-Zero quality |
| R1-Zero | Full RL pipeline | Emergent reasoning |
| Kimi k1.5 | Multi-stage RL | o1-level with vision |

## Three Paradigms

### 1. RL from Scratch (DeepSeek-R1, ORZ)
Apply RL directly to base model with rule-based rewards → emergent chain-of-thought
- **Pro**: Reasoning emerges naturally; no human-annotated reasoning traces needed
- **Con**: Expensive, unstable training; requires careful engineering
- **Key debate**: GRPO vs PPO — ORZ shows PPO is more stable and 10× more efficient

### 2. SFT Distillation (s1)
Fine-tune on curated reasoning traces → budget forcing at inference extends thinking
- **Pro**: Extremely cheap (1K examples, 26 minutes training)
- **Con**: Lower ceiling than RL approaches; depends on quality of distillation data
- **Insight**: Budget forcing (appending "Wait") triggers self-correction

### 3. RL After SFT (Kimi k1.5, Qwen3, Klear-Reasoner)
SFT warm-up → RL to scale further → unified deployment
- **Pro**: Most practical; best final quality
- **Con**: Complex multi-stage pipeline
- **Innovation**: Qwen3's think/no-think fusion; [[sources/klear-reasoner|Klear-Reasoner]]'s GPPO algorithm preserves gradients from clipped tokens
- **Strong results at small scale**: Klear-Reasoner-8B achieves 90.5% AIME24 from Qwen3-8B-Base

### 4. Cross-Domain RL (Guru, General-Reasoner)
Expand RL beyond math/code to diverse domains
- **Pro**: Generalizes to physics, chemistry, finance, logic, etc.
- **Con**: Requires domain-specific verifiable rewards
- **Key insight**: [[sources/guru|Guru]] shows underrepresented domains need in-domain training; [[sources/general-reasoner|General-Reasoner]] replaces brittle string matching with model-based verification

### 5. RL for Open-Ended Tasks (RuscaRL)
Apply RL to domains without automatic verifiers
- **Pro**: Enables RL on medical, writing, instruction-following tasks
- **Con**: Depends on LLM-as-Judge reliability
- **Key insight**: [[sources/ruscarl|RuscaRL]] uses rubric scaffolding with Vygotsky-inspired decay, achieving results that surpass OpenAI o3 on HealthBench

## Key Insights

### 1. Simplicity Wins
All RL teams arrived at similar conclusions: **you don't need** Monte Carlo tree search, value functions (debatable — see ORZ), or process reward models. Simple RL with verifiable rewards is sufficient.

### 2. Multiple Paths to Reasoning
The field has shown at least three viable paths: pure RL, SFT distillation, and RL after SFT. Each has different cost/quality trade-offs.

### 3. Context Length Is a Scaling Axis
Kimi k1.5 demonstrated that training with 128K context during RL improves reasoning. s1's budget forcing achieves similar effects by extending thinking at inference time.

### 4. PPO vs GRPO
ORZ's finding that PPO outperforms GRPO challenges the DeepSeek-R1 recipe. PPO's learned critic provides per-token advantage estimates that identify and devalue repetitive patterns. [[sources/klear-reasoner|Klear-Reasoner]]'s GPPO offers an alternative: keep GRPO but fix the gradient-clipping problem.

### 5. Data Efficiency
s1 shows that just 1,000 carefully curated examples can unlock strong reasoning via SFT. The three criteria (quality, difficulty, diversity) are key for selection.

### 6. Test-Time Compute Theory
[[sources/scaling-test-time-compute|Snell et al. (2024)]] provided the theoretical foundation: compute-optimal test-time strategies depend on prompt difficulty, and a small model with optimal test-time compute can match a 14× larger model.

### 7. RL Is Expanding Beyond Math/Code
[[sources/guru|Guru]], [[sources/general-reasoner|General-Reasoner]], and [[sources/ruscarl|RuscaRL]] demonstrate that RL for reasoning is no longer limited to math/code — cross-domain, open-ended, and agentic tasks are now viable RL targets. [[sources/agentic-rl-reasoning|Agentic RL]] shows that 4B models with proper tool-use RL can surpass 32B models.

### 8. Process Rewards Without Human Labels
[[sources/repro|RePro]] shows that process-level rewards can be derived automatically from ground truth answers (via optimization trajectory analysis), providing a practical middle ground between outcome-only rewards and expensive human-labeled process supervision.

## See Also
- [[comparisons/alignment-methods]] — RLHF vs DPO vs GRPO
- [[comparisons/rl-reasoning-methods]] — Detailed RL methods comparison
- [[concepts/test-time-compute]] — Test-time compute scaling theory
- [[concepts/grpo]]
- [[concepts/process-reward-models]]
- [[concepts/scaling-laws]]
- [[concepts/agents]] — Agentic RL section
