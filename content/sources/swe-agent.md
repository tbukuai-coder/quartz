---
type: source
arxiv_id: "2405.15793"
title: "SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering"
authors: ["John Yang", "Carlos E. Jimenez", "Alexander Wettig", "et al."]
date: 2024-05-24
org: "Princeton"
tags: [agents, code, tool-use, 2024]
upvotes: 7
---

# SWE-agent

> The first **autonomous software engineering agent** that interfaces with a real computer environment — achieving **12.5% on SWE-bench** (2× previous SOTA) by giving LLMs a specialized **Agent-Computer Interface (ACI)** for navigating codebases, editing files, and running tests. Launched the coding agent revolution.

## Key Contributions
- **Agent-Computer Interface (ACI)**: Custom interface optimized for LLM interaction with code repositories — file navigation, search, editing, test execution
- **12.5% on SWE-bench**: Resolved 12.5% of real-world GitHub issues (from 3.8% previous SOTA)
- **Demonstrated interface design matters**: The ACI itself is more important than the underlying LLM
- **87.7% on HumanEvalFix**: Strong on targeted code repair tasks
- **Open-source**: Full agent framework released

## Method
### Agent-Computer Interface (ACI)
Instead of raw bash/terminal, SWE-agent provides structured commands:
- **`find_file`**: Search for files by name across repository
- **`search_dir/search_file`**: Grep-like search with formatted output
- **`open`**: View file with line numbers, automatic windowing
- **`edit`**: Replace lines with validation (syntax checking)
- **`create`**: Create new files
- **`submit`**: Finalize patch

### Key Design Principles
1. **Simplified output**: Format terminal output for LLM parsing (line numbers, truncation)
2. **Error recovery**: Informative error messages guide the agent to fix mistakes
3. **Guardrails**: Prevent common failure modes (editing wrong file, losing context)
4. **Search-first**: Encourage exploration before editing

## Results
| Agent | SWE-bench (%) | HumanEvalFix (%) |
|---|---|---|
| **SWE-agent (GPT-4)** | **12.5** | **87.7** |
| RAG baseline (GPT-4) | 3.8 | — |
| Claude 3 Opus (direct) | 4.8 | — |

## Impact
- Launched the **coding agent** paradigm — SWE-bench became the standard benchmark
- Inspired: Devin, Cursor, Codex CLI, [[sources/codeact|CodeAct]], OpenHands, Aider
- SWE-bench became the most important benchmark for coding agents
- Demonstrated that **interface design** (ACI) is as important as model capability for agents

## Connections
- Related: [[sources/codeact|CodeAct]] (code as actions), [[sources/react|ReAct]] (reasoning + acting)
- Concepts: [[concepts/agents|LLM Agents]], [[concepts/llm-evaluation]]
- Extended by: SWE-agent 2.0, OpenHands, many coding agent frameworks

## Citation
> Yang et al., "SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering," arXiv:2405.15793, 2024.
