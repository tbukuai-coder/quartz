---
type: source
arxiv_id: "2605.02910"
title: "CreativityBench: Evaluating Agent Creative Reasoning via Affordance-Based Tool Repurposing"
authors: null
venue: "arXiv preprint"
year: 2026
date: "2026-05"
upvotes: 18
tags: [agents, evaluation, creativity, affordance, tool-use, benchmarking]
github: "https://github.com/CreativityBench/CreativityBench"
---

# CreativityBench: Evaluating Agent Creative Reasoning via Affordance-Based Tool Repurposing

> The first large-scale benchmark for systematic evaluation of **creative intelligence** in LLMs through **affordance-based creative tool use** — requiring models to repurpose objects based on fine-grained part-level physical attributes rather than semantic plausibility alone.

## Key Contributions

1. **Affordance Knowledge Base**: First structured KB with 4K entities, 26K parts, 288K physical attributes, 125K state attributes, yielding 157K annotated affordances across 8 household scenes
2. **Scalable annotation pipeline**: LLM-assisted top-down decomposition (entity → parts → attributes → affordances) with human-in-the-loop validation
3. **14K benchmark tasks**: Reverse-engineered from affordances — each task requires non-obvious, physically grounded affordance reasoning
4. **Critical findings**: Strong models fail creative tool use; reasoning ≠ creativity; scaling doesn't help; standard inference interventions fail

## Method

### Affordance Knowledge Base Construction

**Hierarchical decomposition**: entity → parts → attributes → affordances

| Component | Count |
|---|---|
| Scenes | 8 |
| Entities | 3,816 |
| Parts | 26,238 |
| Physical attributes | 288,318 |
| State attributes | 124,972 |
| Affordances | 157,427 |

**Two attribute types**:
- **Physical attributes** (A_p): intrinsic, fixed — geometry, material, rigidity, elasticity
- **State attributes** (A_s): variable — accessibility, moisture, temperature, internal state

**Affordance structure**: f = (action, C_u, C_e, C_r)
- C_u: use condition (prep steps needed)
- C_e: environment condition (external prerequisites)
- C_r: recipient condition (constraints on target object)
- **Typicality levels**: normal (intended) vs emergency (repurposed, levels 1–5)

### Task Generation (Reverse Engineering)
Instead of task → find tool, the pipeline starts from **known affordance** → synthesizes scenario where discovering that affordance is the optimal solution. This ensures:
- Well-defined ground-truth reasoning trajectory
- Requires inferring affordance from object attributes alone (not semantic matching)

## Evaluation Metrics

| Metric | What it measures |
|---|---|
| **Gold Correct Rate** | Correct entity AND correct part selected |
| **Entity Correct Rate** | Correct entity selected (regardless of part) |
| **Constraint Coverage** | Use / Environment / Recipient conditions stated |
| **Physical Grounding** | Solution justified by part's physical attributes |
| **Action Feasibility** | Proposed usage is physically plausible |
| **Prediction Correctness** | Overall correctness (LLM-as-Judge, 1–5 scale) |

## Critical Findings

### 1. Part-Level Grounding is the Bottleneck
- Entity correctness: **51.5%** average across models
- Gold correctness (entity + part): **19.1%** average
- **>60% performance drop** from entity to part level
- Models recognize plausible objects but cannot identify the specific part enabling the affordance

### 2. Reasoning ≠ Creativity
- GPT-5.2 achieves highest constraint coverage and action feasibility (strong reasoning)
- But **Qwen3-32B achieves 1.5× gold correctness** (better creative discovery)
- Clear dissociation: systematic reasoning vs novel affordance discovery

### 3. Scaling Doesn't Help Creativity
- Qwen3: 4B → 14B: +30% gold correctness; 14B → 32B: **<5%**
- GPT-5 Nano → Mini: +40%; Mini → 5.2: **only +7%**
- Performance heavily bounded by affordance commonality — rare tool repurposing degrades significantly

### 4. Standard Interventions Fail
- Higher temperature: minimal gain, often exacerbates hallucinations
- Structured CoT: marginal improvement — models commit to incorrect hypotheses early
- Interactive evaluation: reveals premature hypothesis fixation rather than genuine exploration

## Connections

- [[concepts/agents|Agents & Tool Use]] — CreativityBench reveals fundamental gap between tool-using agents and creative agents
- [[sources/agentic-rl-reasoning|Agentic RL]] — Creative tool use requires different training signals than standard reasoning
- [[sources/skill1|Skill1]] — Skill evolution may help discover novel affordances from experience
- [[sources/web2bigtable|Web2BigTable]] — Bi-level agents for information extraction; creative agents for physical problem solving
- [[concepts/llm-evaluation|LLM Evaluation]] — New dimension: creativity evaluation beyond reasoning benchmarks
- [[comparisons/rl-reasoning-methods|RL Reasoning Methods]] — Current RL focuses on verifiable reasoning; creative reasoning is open-ended
