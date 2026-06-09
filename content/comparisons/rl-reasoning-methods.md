---
type: comparison
tags: [reasoning, rl, grpo, ppo, alignment, 2025]
---

# RL Reasoning Methods: Post-DeepSeek-R1 Landscape

> Comparing the explosion of RL approaches for LLM reasoning that followed DeepSeek-R1 — from algorithm variants to data strategies to efficiency techniques.

## Overview
After [[sources/deepseek-r1|DeepSeek-R1]] demonstrated that pure RL produces emergent chain-of-thought reasoning, the field exploded with variants and improvements. This comparison covers the major approaches as of late 2025.

## Algorithm Comparison

| Method | Algorithm | Critic? | Key Innovation | Best Result |
|---|---|---|---|---|
| [[sources/deepseek-r1\|DeepSeek-R1]] | GRPO | No | Pure RL, no SFT needed | Matches o1 at 671B |
| [[sources/open-reasoner-zero\|ORZ]] | PPO | Yes | PPO > GRPO with 10× fewer steps | Strong at 7B–32B |
| [[sources/prorl\|ProRL]] | GRPO+reset | No | Prolonged RL genuinely expands boundaries | No plateau observed |
| [[sources/swe-rl\|SWE-RL]] | GRPO/PPO | No | RL on git evolution data | SOTA SWE-bench |
| [[sources/meta-abilities-alignment\|Meta-Abilities]] | Domain RL + merge | No | Explicit deduction/induction/abduction | More reliable reasoning |
| [[sources/reasoning-vectors\|Reasoning Vectors]] | Task arithmetic | No | Transfer reasoning via weight diff | Zero-cost transfer |
| [[sources/phi-4-reasoning\|Phi-4-reasoning]] | SFT + RL | — | "Teachable" prompt curation | 14B beats 70B |
| [[sources/s1\|s1]] | SFT only | — | 1K examples + budget forcing | Beats o1-preview |
| [[sources/klear-reasoner\|Klear-Reasoner]] | GPPO | No | Gradient-preserving clipping fixes exploration | **90.5% AIME24** at 8B |
| [[sources/repro\|RePro]] | Any (plug-in) | No | Process-level reward via optimization lens | +2.5 AIME24 on Qwen3-1.7B |
| [[sources/guru\|Guru]] | GRPO | No | 6-domain corpus + domain-specific rewards | +7.9% on 17-task suite |
| [[sources/general-reasoner\|General-Reasoner]] | GRPO (Zero RL) | No | Model-based verifier + 230K cross-domain | Matches GPT-4o on GPQA |
| [[sources/ruscarl\|RuscaRL]] | GRPO + rubrics | No | Rubric scaffolding for open-ended RL | Beats o3 on HealthBench |
| [[sources/agentic-rl-reasoning\|Agentic RL]] | GRPO-TCR | No | Real tool-use trajectories + deliberative strategy | 4B beats 32B agentic |
| [[sources/interleaved-reasoning\|Interleaved Reasoning]] | GRPO/PPO/RF++ | No | Interleave think/answer, 80% TTFT reduction | +12.5% accuracy, 37% shorter |
| [[sources/multi-turn-agent-rl\|Multi-Turn Agent RL]] | MT-GRPO/MT-PPO | Yes (PPO) | Turn-level credit assignment for agents | Near-perfect format (99.9%) |
| [[sources/raif\|RAIF]] | GRPO | No | RL for complex instruction following (not math/code) | +2.93% on ComplexBench |
| [[sources/nonsense-helps-lope\|LoPE (Nonsense Helps)]] | GRPO | No | Lorem Ipsum perturbation solves zero-advantage | Restores signal on hard queries |
| [[sources/balanced-aggregation-grpo\|Balanced Aggregation]] | GRPO | No | Fixes sequence vs token aggregation bias | Stable across lengths/phases |
| [[sources/scaling-implicit-deductive-reasoning\|Implicit Deductive Reasoning]] | N/A (theory) | — | Bidirectional masking enables implicit CoT | Comparable to explicit CoT |
| [[sources/skill1\|Skill1]] | GRPO | No | Unified skill selection + utilization + distillation | 97.5% ALFWorld |
| [[sources/resrl\|ResRL]] | GRPO | No | Negative projection residual reweighting decouples pos/neg gradients | +9.4% Avg@16 over NSR on Qwen3-4B; 1469.5 CodeForces rating |

## What Actually Works? ([[sources/tricks-or-traps-rl|Tricks or Traps]])

| Claim | Verdict | Evidence |
|---|---|---|
| GRPO > PPO | **Contested** | ORZ shows PPO better; depends on model/data |
| More RL compute = better | **True (with caveats)** | ProRL shows no plateau; but must avoid reward hacking |
| SFT init matters most | **True** | Tricks or Traps shows init dominates algorithm choice |
| Data quality > quantity | **True** | s1 (1K examples), SWE-RL (natural data) |
| Random rewards work | **False (contamination)** | [[sources/rl-data-contamination\|Data Contamination paper]] exposes benchmark leakage |
| Clipping hurts exploration | **True** | [[sources/klear-reasoner\|Klear-Reasoner/GPPO]] shows gradient preservation fixes this |
| Cross-domain RL generalizes | **Partially** | [[sources/guru\|Guru]] shows it fails for underrepresented domains |
| RL works beyond math/code | **True** | [[sources/ruscarl\|RuscaRL]] (medical, writing), [[sources/general-reasoner\|General-Reasoner]] (physics, finance), [[sources/raif\|RAIF]] (instruction following) |
| Interleaved reasoning helps | **True** | [[sources/interleaved-reasoning\|Interleaved Reasoning]]: +12.5% Pass@1, 80% TTFT reduction |
| Turn-level credit assignment helps | **True** | [[sources/multi-turn-agent-rl\|Multi-Turn Agent RL]]: stable training, 99.9% format correctness |
| Nonsense perturbations help | **True** | [[sources/nonsense-helps-lope\|LoPE]]: surprisingly effective at restoring signal on zero-advantage queries |
| Sequence vs token aggregation matters | **True** | [[sources/balanced-aggregation-grpo\|Balanced Aggregation]]: neither pure sequence nor pure token is optimal |
| Implicit reasoning approaches explicit CoT | **True (with depth limits)** | [[sources/scaling-implicit-deductive-reasoning\|Implicit Deductive Reasoning]]: bidirectional masking enables implicit reasoning comparable to explicit CoT, but depth extrapolation still requires CoT |
| Unified skill evolution works | **True** | [[sources/skill1\|Skill1]]: single-policy co-evolution of selection, utilization, distillation outperforms piecewise approaches |
| Decoupling pos/neg gradients improves RL | **True** | [[sources/resrl\|ResRL]]: projection-residual reweighting preserves shared valid tokens while suppressing errors; outperforms NSR on Avg@16 and Pass@128 simultaneously |

## ⚠️ Data Contamination Warning

[[sources/rl-data-contamination|Wu et al. (2025)]] showed that many RL reasoning improvements on Qwen2.5 are artifacts of benchmark contamination in pretraining data. Results should be verified on:
- Multiple model families (not just Qwen2.5)
- Fresh benchmarks (not MATH-500/AMC/AIME)
- Leakage-free evaluations (RandomCalculation, etc.)

## GRPO Training Improvements (2026)

Three recent papers from May 2026 systematically fix GRPO training pathologies:

### Zero-Advantage Problem (LoPE)

[[sources/nonsense-helps-lope|LoPE (2026)]] identifies a critical failure mode: when **all sampled rollouts for a query fail**, the group-relative advantage collapses to zero — the model receives no training signal. This wastes data and compute on hard queries where the model needs training most.

**Fix**: Inject Lorem Ipsum-style nonsense perturbations into the prompt space during rollout generation. This creates artificial success/failure variance where none existed. The perturbed outputs are filtered via perplexity scores and assembled stochastically.

Key insight: the model learns to ignore the noise while benefiting from the restored gradient signal. No performance degradation on clean queries.

### Sequence vs Token Aggregation Bias (Balanced Aggregation)

[[sources/balanced-aggregation-grpo|Balanced Aggregation (2026)]] analyzes how token-level policy gradients are aggregated within each group — a design choice that was never systematically studied:

| Aggregation | Bias | When it fails |
|---|---|---|
| **Sequence aggregation** (standard GRPO) | Averages over all tokens; underweights long sequences | Long reasoning chains get diluted gradients |
| **Token aggregation** (recent alternative) | Normalizes per-token; unstable early in training | Early training collapse, high variance |
| **Balanced aggregation** (proposed) | Interpolates based on group statistics | Stable across training phases and sequence lengths |

The balanced approach dynamically interpolates between the two based on group statistics, improving training stability and final performance across reasoning and code benchmarks.

### Positive-Negative Gradient Conflict (ResRL)

[[sources/resrl|ResRL (2026)]] addresses a deeper problem in GRPO/NSR: when negative sample reinforcement penalizes incorrect trajectories, it **inadvertently suppresses shared valid tokens** that also appear in correct trajectories. This gradient conflict limits both Pass@1 and Pass@k performance.

**Fix**: Confine penalties to gradient directions **orthogonal to the positive subspace**:
1. Construct positive subspace S from top-k SVD of positive token representations
2. Compute orthogonal-complement energy: $e(x) = (1/d) \|(I - P_S)x\|^2$
3. Reweight negative sample advantages by e(x) — higher residual = more orthogonal = stronger penalty
4. Add length-scaled reward discount beyond 3500 tokens to curb verbosity

**Results**: +9.4% Avg@16 over NSR on Qwen3-4B math; +9.6% CodeForces rating; +10.4% ALFWorld over EMPG. Best at rank k=64 (protection-discrimination sweet spot). Pass@128 improves simultaneously — unlike NSR which trades off Pass@1 vs Pass@k.

## Agentic RL: From Tool-Use to Skill Evolution

The agentic RL subfield has expanded from basic tool-use to sophisticated credit assignment and skill lifecycle management:

| Paper | Focus | Algorithm | Key Innovation | Result |
|---|---|---|---|---|
| [[sources/agentic-rl-reasoning\|Agentic RL]] | Tool-use recipes | GRPO-TCR | Real trajectories + deliberative strategy | 4B beats 32B |
| [[sources/multi-turn-agent-rl\|Multi-Turn Agent RL]] | Credit assignment | MT-GRPO/MT-PPO | Turn-level advantages | 99.9% format |
| [[sources/a2tgpo-agentic\|A²TGPO]] | Turn-level clipping | A²TGPO | Adaptive turn-group optimization | Improved multi-turn agents |
| [[sources/opensearch-vl\|OpenSearch-VL]] | Multimodal search | Fatal-aware GRPO | Composite reward + fatal masking | 63.7 avg across 7 benchmarks |
| [[sources/skill1\|Skill1]] | Skill lifecycle | GRPO | Unified selection + utilization + distillation | 97.5% ALFWorld |
| [[sources/skillos\|SkillOS]] | Skill curation | RL (various) | Frozen executor + trainable curator via composite reward | +9.8% relative over strongest baseline |

### Unified Skill Evolution (Skill1)

[[sources/skill1|Skill1 (2026)]] represents a breakthrough in agent training by co-evolving all three stages of the skill lifecycle with a single policy and shared task-outcome signal:

**The Three Stages**:
1. **Skill Selection**: Generate query → retrieve candidates → re-rank via policy → select best skill
2. **Skill Utilization**: Multi-turn environment interaction conditioned on selected skill
3. **Skill Distillation**: Reflect on trajectory → produce reusable strategy + scenario description → admit to library on success

**Credit Assignment Decomposition**:
- **Utilization**: Direct outcome $R_i^{\text{util}} = r(\tau_i)$
- **Selection**: NDCG-based re-ranking reward against per-skill utility trends (EMA of outcomes)
- **Distillation**: $R_i^{\text{distill}} = r(\tau_i) - \hat{U}_i$ — is this experience better than what we already know?

**Key Result**: 97.5% on ALFWorld (+2.6 over RetroAgent), with ablations showing removing the library causes a **-16.6 point drop** and removing any credit signal degrades all three capabilities — confirming mutual dependence.

### Skill Curation (SkillOS)

[[sources/skillos|SkillOS (2026)]] addresses the critical gap of **skill curation** — how agents manage, update, and prune skill collections over time for long-term proficiency:

- **Architecture**: Frozen executor (solves tasks with BM25-retrieved skills) + trainable curator (manages Markdown skill repo via insert/update/delete)
- **Training**: Task groups for long-term utility + composite reward (performance + valid ops + skill quality + repo compactness)
- **Result**: +9.8% relative improvement and −6.0% fewer steps vs strongest baseline; 8B curator outperforms Gemini-2.5-Pro
- **Generalization**: Curator transfers across executors (Qwen3-8B → Gemini-2.5-Pro) and task domains

## Training Data Strategies

| Strategy | Source | Key Finding |
|---|---|---|
| Competition math | DeepSeek-R1, ORZ | Good for math but narrow |
| Software evolution | [[sources/swe-rl\|SWE-RL]] | Generalizes beyond code to math/reasoning |
| Automatic task gen | [[sources/meta-abilities-alignment\|Meta-Abilities]] | Enables targeted meta-ability training |
| Curated "teachable" prompts | [[sources/phi-4-reasoning\|Phi-4-reasoning]] | Quality+diversity of SFT data critical |
| Cross-domain corpus (6 domains) | [[sources/guru\|Guru]] | Domain-specific rewards needed; in-domain training essential for underrepresented domains |
| Cross-domain verifiable (230K) | [[sources/general-reasoner\|General-Reasoner]] | Model-based verifier beats rule-based matching; Zero RL generalizes across domains |
| Real agentic trajectories | [[sources/agentic-rl-reasoning\|Agentic RL]] | End-to-end tool-use trajectories far superior to synthetic/stitched data |
| Rubric-guided open-ended | [[sources/ruscarl\|RuscaRL]] | LLM-as-Judge rubrics enable RL on medical, writing, instruction tasks |
| Complex instruction evolving | [[sources/raif\|RAIF]] | LLM-based constraint instantiation + code/LLM verification for instruction following |
| Multi-hop interleaving | [[sources/interleaved-reasoning\|Interleaved Reasoning]] | Conditional intermediate rewards for think-answer alternation |
| Turn-level search feedback | [[sources/multi-turn-agent-rl\|Multi-Turn Agent RL]] | Retrieval quality per turn provides dense credit assignment |
| Nonsense perturbation for hard queries | [[sources/nonsense-helps-lope\|LoPE]] | Restores training signal when all rollouts fail |
| Balanced gradient aggregation | [[sources/balanced-aggregation-grpo\|Balanced Aggregation]] | Interpolates sequence vs token aggregation based on group stats |
| Unified skill co-evolution | [[sources/skill1\|Skill1]] | Single-policy optimization of selection + utilization + distillation via decomposed task-outcome signal |
| Skill curation via RL | [[sources/skillos\|SkillOS]] | Long-term utility composite reward for managing skill repositories over streaming tasks |
| Gradient decoupling pos/neg | [[sources/resrl\|ResRL]] | Projection-residual reweighting preserves shared valid reasoning while suppressing errors |

## Efficiency Techniques

| Technique | Paper | Benefit |
|---|---|---|
| Confidence filtering | [[sources/deepconf\|DeepConf]] | 30–50% fewer tokens |
| Budget forcing | [[sources/s1\|s1]] | Controls thinking budget |
| Reasoning vectors | [[sources/reasoning-vectors\|Reasoning Vectors]] | Zero additional training |
| Process reward (RePro) | [[sources/repro\|RePro]] | Shorter, more efficient reasoning chains |
| Gradient-preserving clipping | [[sources/klear-reasoner\|Klear-Reasoner/GPPO]] | Faster convergence |
| Rubric scaffolding decay | [[sources/ruscarl\|RuscaRL]] | Models internalize reasoning, no external crutches needed |
| Interleaved reasoning | [[sources/interleaved-reasoning\|Interleaved Reasoning]] | 80% TTFT reduction, 37% shorter chains |
| Turn-level rewards | [[sources/multi-turn-agent-rl\|Multi-Turn Agent RL]] | Stable multi-turn training, faster convergence |
| Deep reasoning for instructions | [[sources/raif\|RAIF]] | Teaches reasoning structure for constraint satisfaction |
| Nonsense perturbation | [[sources/nonsense-helps-lope\|LoPE]] | Restores signal on hard queries without degradation |
| Balanced aggregation | [[sources/balanced-aggregation-grpo\|Balanced Aggregation]] | Stable training across sequence lengths |
| Gradient decoupling | [[sources/resrl\|ResRL]] | Improves Pass@1 and Pass@k simultaneously; stable with low-variance updates |

## Expanding RL Beyond Math/Code

A key theme in 2025 is **breaking the math/code monopoly** in RLVR:

| Paper | Domains Covered | Key Innovation |
|---|---|---|
| [[sources/guru\|Guru]] | Math, Code, Science, Logic, Simulation, Tabular | Domain-specific verifiable rewards for 6 domains |
| [[sources/general-reasoner\|General-Reasoner]] | Physics, Chemistry, Finance, Electronics, Humanities | Model-based answer verifier replaces string matching |
| [[sources/ruscarl\|RuscaRL]] | Medical, Writing, Instruction Following | Rubric-based rewards for open-ended tasks |
| [[sources/agentic-rl-reasoning\|Agentic RL]] | Math, Code, Science (with tool use) | Real multi-turn tool-use trajectories |
| [[sources/raif\|RAIF]] | Complex instruction following (And, Chain, Selection, Nested) | RL for compositional constraint satisfaction |
| [[sources/interleaved-reasoning\|Interleaved Reasoning]] | Multi-hop QA, math, science | Interleave thinking/answering for efficiency + accuracy |
| [[sources/multi-turn-agent-rl\|Multi-Turn Agent RL]] | Search, tool use, multi-hop QA | Turn-level credit assignment for agent trajectories |
| [[sources/skill1\|Skill1]] | Household planning, online shopping | Unified skill evolution via shared task-outcome decomposition |
| [[sources/resrl\|ResRL]] | Math, Code, Agents, Function Calling | Gradient decoupling improves all domains simultaneously |

## Implicit vs Explicit Reasoning

[[sources/scaling-implicit-deductive-reasoning|Implicit Deductive Reasoning (2026)]] introduces a new dimension to the reasoning debate: can Transformers perform implicit deductive reasoning comparable to explicit chain-of-thought?

**Findings**:
- In sufficiently deep models with **bidirectional prefix masking**, implicit reasoning approaches explicit CoT performance across diverse graph topologies and problem sizes
- **Algorithmic alignment** (matching model inductive biases to reasoning structure) is critical — without it, models exploit spurious features
- However, **explicit CoT remains necessary for depth extrapolation** (reasoning beyond training depth)
- This has implications for diffusion language models and other non-autoregressive architectures where CoT is not naturally available

## Recommended Reading Order
1. [[sources/rl-reasoning-survey|RL Survey]] — comprehensive overview
2. [[sources/tricks-or-traps-rl|Tricks or Traps]] — what actually works
3. [[sources/rl-data-contamination|Data Contamination]] — evaluation pitfalls
4. [[sources/prorl|ProRL]] + [[sources/swe-rl|SWE-RL]] — pushing the frontier
5. [[sources/klear-reasoner|Klear-Reasoner]] — practical post-training recipe with GPPO
6. [[sources/guru|Guru]] + [[sources/general-reasoner|General-Reasoner]] — cross-domain RL
7. [[sources/ruscarl|RuscaRL]] — RL for open-ended tasks
8. [[sources/agentic-rl-reasoning|Agentic RL]] — RL for tool-using agents
9. [[sources/interleaved-reasoning|Interleaved Reasoning]] — efficiency in reasoning
10. [[sources/multi-turn-agent-rl|Multi-Turn Agent RL]] — multi-turn credit assignment
11. [[sources/raif|RAIF]] — RL for instruction following
12. [[sources/nonsense-helps-lope|LoPE]] — fixing the zero-advantage problem
13. [[sources/balanced-aggregation-grpo|Balanced Aggregation]] — fixing aggregation bias
14. [[sources/resrl|ResRL]] — decoupling positive-negative gradient interference
15. [[sources/scaling-implicit-deductive-reasoning|Implicit Deductive Reasoning]] — implicit vs explicit reasoning theory
16. [[sources/skill1|Skill1]] — unified skill evolution for agents
17. [[sources/skillos|SkillOS]] — skill curation for self-evolving agents


## Scaling Laws for RL Reasoning: ScaleLogic

[[sources/scalelogic|ScaleLogic (2026)]] provides the first rigorous study of how RL training scales with reasoning complexity:

- **Power-law scaling**: Training compute T ∝ D^γ (R² > 0.99) where D is reasoning depth
- **Expressiveness determines γ**: Implication-only (1.04) → +Conjunction (1.22) → +Negation (1.47) → +Disjunction (1.71) → +Quantification (2.60)
- **Key insight**: What you train on matters more than how much — more expressive logical training yields both larger gains (+10.66 points) and faster convergence on downstream benchmarks
- **Cross-algorithm robustness**: Power law holds across DAPO, GRPO, REINFORCE++ (γ varies by <0.04)
- **Curriculum helps**: ~3× more compute-efficient than fixed-depth training

This establishes **logical expressiveness as a scaling dimension** for RL reasoning — complementing existing knowledge about data volume and model size.

## See Also
- [[comparisons/reasoning-models|Reasoning Models]] (model-level comparison)
- [[comparisons/alignment-methods|Alignment Methods]] (RLHF vs DPO vs GRPO)
- [[concepts/grpo|GRPO]]
- [[concepts/test-time-compute|Test-Time Compute]]
- [[concepts/agents|Agents & Tool Use]]
- [[concepts/process-reward-models|Process Reward Models]]
