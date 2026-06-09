---
type: source
arxiv_id: "2605.18747"
title: "Code as Agent Harness"
authors: ["Xuying Ning", "Katherine Tieu", "Dongqi Fu", "Tianxin Wei", "Zihao Li", "Yuanchen Bei", "Jiaru Zou", "Mengting Ai", "Zhining Liu", "Ting-Wei Li"]
date: 2026-05-19
org: "Multi-institution"
tags: [agents, code, infrastructure, survey, 2026]
upvotes: 211
---

# Code as Agent Harness

> Survey and framework positioning code as the unified operational substrate for agent reasoning, acting, environment modeling, planning, memory, tool use, feedback-driven control, optimization, and multi-agent coordination.

## Key Contributions
- **Code as Agent Harness framework**: unifies how code serves as operational substrate across all agent capabilities (not just code generation target)
- **Taxonomy of code roles**: reasoning substrate, action execution, environment modeling, planning medium, memory structure, tool interface, feedback channel, optimization target, coordination protocol
- **Survey of agentic systems**: comprehensive coverage of how code infrastructure enables LLM agents across DevOps, enterprise workflows, scientific discovery, and software engineering
- **317 GitHub stars** for the awesome-list companion resource

## Method
The paper reframes the relationship between LLMs and code in agentic systems. Rather than treating code as merely an output target (as in code generation benchmarks), it identifies code as the unified infrastructure layer that enables agent capabilities: structured reasoning via executable programs, action execution via API calls, environment modeling via simulators, planning via program synthesis, memory via data structures, tool use via function interfaces, feedback via test execution, and coordination via protocols.

## Results
- Comprehensive taxonomy covering 9 code roles in agentic systems
- Analysis of limitations and open problems in code-based agent infrastructure
- Roadmap for future code-agent research directions

## Connections
- Builds on: [[sources/codeact]], [[sources/react]], [[sources/toolformer]]
- Related: [[sources/skillopt]], [[sources/autoresearchclaw]], [[sources/swe-agent]]
- Related concepts: [[concepts/agents]], [[concepts/structured-generation]], [[comparisons/code-models-agents]]

## Citation
> Ning et al., "Code as Agent Harness," arXiv:2605.18747, 2026.
