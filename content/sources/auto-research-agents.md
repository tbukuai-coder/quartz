---
type: source
arxiv_id: "2605.05724"
title: "Auto Research with Specialist Agents Develops Effective and Non-Trivial Training Recipes"
authors: ["Jingjie Ning", "Xiaochuan Li", "Ji Zeng", "Hao Kang", "Chenyan Xiong"]
venue: "arXiv preprint"
year: 2026
date: "2026-05"
org: "Carnegie Mellon University"
upvotes: 10
tags: [agents, automl, research-automation, training-recipes, empirical-loop]
github: "https://github.com/cxcscmu/Auto-Research-Recipes"
---

# Auto Research with Specialist Agents Develops Effective and Non-Trivial Training Recipes

> A closed empirical loop where **specialist agents partition recipe surfaces and share measured lineage** across trials — autonomously developing training recipes that reduce Parameter Golf validation bpb by 0.81%, raise NanoChat-D12 CORE by 38.7%, and reduce CIFAR-10 Airbench96 wallclock by 4.59%, all without human intervention during search.

## Key Contributions

1. **Auto research as closed empirical loop**: Not paper generation or single checkpoints, but auditable trajectories of proposals, code diffs, experiments, scores, and failure labels
2. **Specialist agents with shared lineage**: Agents partition the recipe surface (architecture, optimization, augmentation, schedule) and share measured outcomes across all trials — feedback from failures drives later program-level edits
3. **1,197 headline trials fully autonomous**: After one-time setup, humans did not choose proposals, edit recipes, override scores, or repair failed trials
4. **Program-level recipe edits**: Not just hyperparameter tuning — agents rewrite attention kernels, change training schedules, and restructure architectures
5. **Three diverse environments**: Parameter Golf (language model), NanoChat-D12 (chat model), CIFAR-10 Airbench96 (vision) — demonstrating generality

## Method

### The Closed Empirical Loop
```
Hypothesis → Code Edit → Submit Trial → Evaluator Measures → Feedback → Next Proposal
```

Each trial carries:
- A hypothesis (what to test)
- An executable code edit (diff)
- An evaluator-owned outcome (score + legality)
- Feedback that shapes the next proposal (including crashes, budget overruns, failures)

### Specialist Roles
| Environment | Specialists |
|---|---|
| Parameter Golf | Architecture, Optimization, Schedule, Tokenizer |
| NanoChat-D12 | Architecture, Data-Mix, Training-Schedule, Post-training |
| CIFAR-10 | Architecture, Augmentation, Optimization, Schedule |

### Shared Lineage
- **LEADERBOARD.md**: Best-so-far scores visible to all agents
- **KNOWLEDGE.md**: Curated tree of what worked, what failed, and why
- **Failure labels**: Crashes, budget overruns, accuracy-gate misses all become actionable feedback
- Without lineage: proposal-entropy drops and improvements stall (ablation confirms)

### Key Design Principles
- **External measurement**: Evaluator owns the score — agents cannot self-report
- **Affordable iteration**: Each trial costs <$2 compute, enabling hundreds of experiments
- **Architecture-domain audit**: 157 submissions audited for rule compliance
- **Anti-anchoring**: Banlist prevents agents from repeatedly trying failed approaches

## Results

### Headline Improvements
| Environment | Metric | Improvement | Trials |
|---|---|---|---|
| Parameter Golf | Validation bpb | **−0.81%** (1.0810 → 1.0722) | 472 |
| NanoChat-D12 | CORE score | **+38.7%** (0.1618 → 0.2244) | 384 |
| CIFAR-10 Airbench96 | Wallclock | **−4.59%** (26.36s → 25.15s) | 341 |

### Example Program Rewrites (Not Just Hyperparameter Tuning)
- **Parameter Golf**: Attention kernel path change, custom SentencePiece configuration, recurrence-path modifications
- **NanoChat-D12**: Sliding-window attention tuning, data mixture rebalancing, post-training recipe changes
- **CIFAR-10**: Augmentation pipeline restructuring, optimizer schedule rewrites

### Lineage Ablation
- Without shared lineage: improvement rate drops significantly
- Lineage feedback is the mechanism that turns failures into future successes
- Proposal diversity (measured by entropy) is higher with lineage than without

## Connections

- [[sources/intern-atlas|Intern-Atlas]] — Methodological evolution graphs for AI scientists; Auto Research automates the empirical refinement loop
- [[sources/ai-co-mathematician|AI Co-Mathematician]] — Both use hierarchical agents for research; Auto Research focuses on ML training recipe development
- [[sources/agent-native-research-artifact|Ara]] — Auditable research trajectories align with Ara's vision of executable knowledge
- [[concepts/agents|LLM Agents]] — Specialist agents as ML researchers
- [[sources/davinci-llm|daVinci-LLM]] — Data Darwinism framework; Auto Research automates the training recipe search that daVinci studies theoretically
