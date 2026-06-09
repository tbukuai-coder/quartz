---
type: source
arxiv_id: "2605.06614"
title: "SkillOS: Learning Skill Curation for Self-Evolving Agents"
authors: null
venue: "arXiv preprint"
year: 2026
date: "2026-05"
upvotes: 4
tags: [agents, skills, reinforcement-learning, self-evolution, memory, streaming]
github: null
---

# SkillOS: Learning Skill Curation for Self-Evolving Agents

> An experience-driven RL training recipe that learns **skill curation** for self-evolving agents — a frozen executor solves tasks with skills from a Markdown-based SkillRepo, while a trainable curator learns to insert, update, and delete skills based on long-term utility feedback.

## Key Contributions

1. **Modular multi-agent framework**: Frozen executor + trainable curator — decouples execution from skill management
2. **Markdown skill representation**: Skills as YAML-frontmatter + Markdown instruction files (SKILL.md format), managed via file I/O operations like an OS
3. **Long-term utility grounding**: Training instances as groups of related tasks — skills induced from earlier experiences are evaluated by later tasks
4. **Composite reward design**: Task performance + valid function calls + skill quality + SkillRepo compactness
5. **Strong results**: Up to **+9.8% relative performance** and **−6.0% fewer interaction steps** vs strongest baseline; curator generalizes across executors (even Gemini-2.5-Pro)

## Method

### System Architecture

**Skill Repository (SkillRepo)**: External collection of reusable skills
- Format: Markdown files with YAML frontmatter (name, when-to-use description) + instructions (workflows, constraints, heuristics)
- Operations: `insert_skill`, `update_skill`, `delete_skill`

**Agent Executor (π_L)**: Frozen LLM that:
- Retrieves relevant skills via BM25
- Solves tasks conditioning on observation + retrieved skills

**Skill Curator (π_S)**: Trainable model that:
- Observes trajectory ξ_t, correctness indicator, related skills
- Generates curation operations c_t

### RL Training Recipe

**Key Design 1: Task Groups for Long-Term Utility**
- Each training instance = group of related tasks (mimics streaming settings)
- Skills from earlier tasks improve later tasks → grounded long-term utility signal
- Prevents short-term reward hacking

**Key Design 2: Composite Reward**
- **Task performance**: Success rate on current task
- **Valid function calls**: Penalizes malformed curation operations
- **Skill quality**: Reusability and correctness of generated skills
- **Repo compactness**: Rewards pruning redundant/obsolete skills

### Results

### ALFWorld (6 subsets, 3 executors)

| Curator | Executor | Avg. SR | Avg. Steps |
|---|---|---|---|
| None | Qwen3-8B | 47.9% | 21.1 |
| ReasoningBank | Qwen3-8B | 55.7% | 20.1 |
| MemP | Qwen3-8B | 49.7% | 21.0 |
| SkillOS-base | Qwen3-8B | 53.1% | 20.4 |
| **SkillOS** | **Qwen3-8B** | **62.8%** | **18.8** |
| SkillOS-gemini | Gemini-2.5-Pro | 54.3% | 20.8 |
| **SkillOS** | **Gemini-2.5-Pro** | **61.2%** | **18.5** |

- **+9.8%** relative improvement over strongest baseline (ReasoningBank)
- **−6.0%** fewer interaction steps
- 8B curator **outperforms Gemini-2.5-Pro** when used as curator

### Generalization
- Trained curator improves **different executors** (Qwen3-8B → Gemini-2.5-Pro)
- Improves **different task domains** (ALFWorld → single-turn reasoning)
- Skills evolve into **richly structured Markdown** encoding higher-level meta-skills over time

### Ablations
- Removing task grouping (no long-term utility): −3.2% SR
- Removing compactness reward: +12% repo size, −1.8% SR (bloated repo hurts retrieval)
- Removing valid function call reward: −2.1% SR (malformed operations waste steps)

## Connections

- [[sources/skill1|Skill1]] — Unified skill selection + utilization + distillation; SkillOS focuses on curation (the missing piece)
- [[sources/web2bigtable|Web2BigTable]] — Bi-level multi-agent search; SkillOS bi-level executor/curator for skill management
- [[sources/eywa|Eywa]] — Heterogeneous scientific agent framework; SkillOS for general agent skill evolution
- [[sources/agentic-rl-reasoning|Agentic RL]] — RL for tool-using agents; SkillOS applies RL to skill memory management
- [[sources/multi-turn-agent-rl|Multi-Turn Agent RL]] — Turn-level credit assignment; SkillOS uses episode-level credit for skill curation
- [[concepts/agents|Agents & Tool Use]] — Skill curation as essential component of self-evolving agents
- [[concepts/rag|RAG]] — SkillRepo as specialized retrieval-augmented generation for agent capabilities
