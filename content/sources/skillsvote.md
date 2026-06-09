---
type: source
arxiv_id: "2605.18401"
title: "SkillsVote: Lifecycle Governance of Agent Skills from Collection, Recommendation to Evolution"
authors: ["Hongyi Liu", "Haoyan Yang", "Tao Jiang", "Bo Tang", "Feiyu Xiong", "Zhiyu Li"]
date: 2026-05-19
org: "MemTensor"
tags: [agents, skills, governance, lifecycle, 2026]
upvotes: 126
---

# SkillsVote: Lifecycle Governance of Agent Skills from Collection, Recommendation to Evolution

> Lifecycle-governance framework for agent skill ecosystems — managing collection (trajectory decomposition), recommendation (agentic library search), and evolution (evidence-gated updates) of reusable executable + procedural skill artifacts.

## Key Contributions
- **Agent Skills as experience schema**: couples executable scripts with non-executable procedural guidance, including environment requirements and verifiability
- **Skill Collection via trajectory decomposition**: decomposes raw agent trajectories into reusable skill artifacts with environment annotations
- **Skill Recommendation via agentic library search**: retrieves relevant skills for new tasks via structured matching against skill metadata
- **Skill Evolution via evidence-gated updates**: only updates skills when execution evidence supports improvement — prevents context pollution
- **Terminal-Bench 2.0 and SWE-Bench Pro** evaluation demonstrating governance benefits
- **269 GitHub stars**

## Method
SkillsVote treats open skill ecosystems as requiring governance because they contain redundant, uneven, environment-sensitive artifacts. The framework manages three lifecycle phases: (1) Collection — raw trajectories are decomposed into structured skills with executable scripts and procedural guidance; (2) Recommendation — an agentic library search matches task requirements against skill metadata; (3) Evolution — evidence-gated voting mechanism only admits updates when execution evidence demonstrates improvement over existing skills.

## Results
- Significant improvement on Terminal-Bench 2.0 and SWE-Bench Pro
- Prevents skill pollution from indiscriminate updates
- Maintains high-quality skill libraries over long agent lifetimes

## Connections
- Builds on: [[sources/skillopt]], [[sources/skill1]], [[sources/skillos]]
- Related: [[sources/code-as-agent-harness]], [[sources/creativitybench]], [[concepts/agents]]
- Extends the agent skill lifecycle: SkillOpt (optimization) → Skill1 (co-evolution) → SkillOS (curation) → SkillsVote (governance)

## Citation
> Liu et al., "SkillsVote: Lifecycle Governance of Agent Skills from Collection, Recommendation to Evolution," arXiv:2605.18401, 2026.
