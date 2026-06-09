---
type: comparison
tags: [code, agents, models, synthesis]
---

# Comparison: Code Models & Coding Agents

> From **code completion to autonomous software engineering** — tracing the evolution from StarCoder and Code Llama (code generation) through Qwen2.5-Coder (SOTA code models) to SWE-agent and Devin (autonomous coding agents). The code domain has seen the fastest capability growth in AI.

## Overview

The code AI landscape spans two distinct paradigms: (1) **Code LLMs** that generate, complete, and explain code, and (2) **Coding Agents** that autonomously navigate repositories, write patches, and fix bugs. The two are converging — modern agents use code LLMs as their backbone, and code LLMs increasingly incorporate agentic capabilities.

## Code Model Comparison

| Model | Year | Org | Params | HumanEval | Training Data | Key Feature |
|---|---|---|---|---|---|---|
| [[sources/starcoder\|StarCoder]] | 2023 | BigCode | 15.5B | 33.6% | The Stack (1T) | Permissive license, FIM |
| [[sources/code-llama\|Code Llama]] | 2023 | Meta | 7–34B | 48.8% (34B) | Llama 2 + code | Infilling, instruct |
| [[sources/starcoder-2\|StarCoder 2]] | 2024 | BigCode | 3–15B | 46.3% (15B) | Stack v2 (4.3T) | Repo-context, GQA |
| [[sources/qwen25-coder\|Qwen2.5-Coder]] | 2024 | Alibaba | 0.5–32B | 92.7% (32B) | 5.5T tokens | SOTA, 3-stage training |
| DeepSeek-Coder-V2 | 2024 | DeepSeek | 236B MoE | 90.2% | Proprietary | MoE code specialist |

### Key Insight: The Rapid Quality Jump
HumanEval pass@1 progression for best open models:
- 2023: ~34% (StarCoder) → ~49% (Code Llama 34B)
- 2024: ~46% (StarCoder2-15B) → **~93% (Qwen2.5-Coder-32B)**
- Near-perfect code generation in 18 months.

## Coding Agent Comparison

| Agent | Year | Backbone | SWE-bench | Key Innovation |
|---|---|---|---|---|
| RAG baseline | 2024 | GPT-4 | 3.8% | Simple retrieval + generation |
| [[sources/swe-agent\|SWE-agent]] | 2024 | GPT-4 | 12.5% | Agent-Computer Interface (ACI) |
| Devin | 2024 | Proprietary | ~14% | Fully autonomous IDE |
| OpenHands | 2024 | Various | ~20% | Open-source agent framework |
| [[sources/llama-nemotron\|LN-Ultra]] | 2025 | 253B | Strong | Reasoning + code via GRPO |
| Claude 3.5 Sonnet | 2024 | Proprietary | ~49% | Computer use capabilities |

### Agent vs. Model
| Dimension | Code Model | Coding Agent |
|---|---|---|
| **Task** | Single function/file generation | Multi-file repository changes |
| **Context** | Prompt + file | Full repo + tests + issue |
| **Tools** | None (pure generation) | File system, terminal, tests |
| **Evaluation** | HumanEval, MBPP | SWE-bench, SWE-bench Verified |
| **Autonomy** | Single-turn | Multi-step with feedback loops |

## Training Data Approaches

| Approach | Used By | Scale | Advantage |
|---|---|---|---|
| **Permissive code** | StarCoder, BigCode | The Stack (86–619 langs) | Legal clarity, opt-out |
| **All GitHub code** | Code Llama, DeepSeek | Undisclosed | More data, better coverage |
| **Synthetic code** | Qwen2.5-Coder, Phi | LLM-generated | Quality targeting, decontamination |
| **Agent trajectories** | SWE-Master, CoderForge | Task-solution pairs | Agent-specific behavior |

## Code Generation Beyond Text: GPU Kernels

[[sources/kernelbenchx|KernelBench-X (2026)]] introduces a new frontier for code generation: **LLM-generated GPU kernels**. This tests whether LLMs can generate high-performance Triton/CUDA code:

- **176 tasks across 15 categories**: Matrix ops, reduction, scan, attention, quantization, etc.
- **Three key findings**:
  1. **Task structure determines correctness more than method design** — the inherent complexity of the task dominates over prompting strategy
  2. **Iterative refinement improves correctness at the expense of performance** — self-correction helps compile but hurts optimization
  3. **Correctness does not guarantee efficiency** — many correct kernels are far from optimal
- Implication: code generation for performance-critical domains requires different evaluation than text-based code

## Biomedical Tool-Calling: A Specialized Agent Domain

[[sources/biotool-medical|BioTool (2026)]] shows that **domain-specific tool-calling datasets** are essential for specialized agent performance:
- LLMs perform poorly on biomedical tasks because they cannot leverage tools clinical experts use daily (NCBI, Ensembl, UniProt)
- BioTool provides comprehensive biomedical tool-calling dataset covering genomics, proteomics, evolution research
- Fine-tuned models outperform commercial biomedical LLM tools
- **Lesson**: general tool-calling datasets improve generic capabilities, but domain-specific tool datasets are needed for specialized deployment

## Agentic Search: Direct Corpus Interaction

[[sources/dci-agent-retrieval|DCI Agent (2026)]] rethinks how coding agents (and agents generally) access information:
- **Problem**: Standard retrievers compress corpus access into a single top-k step — insufficient for complex multi-step reasoning
- **Solution**: Give agents **terminal-style access to raw text** (grep, browse, pattern matching, iterative exploration)
- The agent uses its reasoning to navigate the corpus rather than relying on pre-computed similarity scores
- Evaluated on BEIR, BrowseComp-Plus, and multi-hop QA — outperforms traditional retrieval on complex tasks
- Implication for code agents: repository search may benefit from direct file system interaction rather than semantic retrieval alone

## AI App-Building Platforms: SWE-WebDevBench

[[sources/swe-webdevbench|SWE-WebDevBench (2026)]] extends evaluation beyond code generation to **full software agency**:
- **68 metrics** across 7 groups: Business Intent, Schema, Frontend, Backend, Security, Performance, Modification
- Evaluates 6 platforms as virtual software development agencies
- **No platform exceeds 60%** overall; every platform has ≥1 metric below 15%
- Key finding: **Specification bottleneck** — platforms compress rich requirements into oversimplified plans; more PM questions → better canary retention (100% vs 21%)
- Production readiness requires 12–60 developer-hours post-generation; security universally poor (<65%)

## Automated Training Recipe Development

[[sources/auto-research-agents|Auto Research with Specialist Agents (2026)]] automates the empirical ML research loop:
- Specialist agents partition recipe surfaces (architecture, optimization, augmentation, schedule) and share measured lineage
- 1,197 fully autonomous trials across 3 environments — no human intervention during search
- **Program-level rewrites**, not just hyperparameter tuning (attention kernels, training schedules, architecture restructuring)
- Results: −0.81% bpb (Parameter Golf), +38.7% CORE (NanoChat-D12), −4.59% wallclock (CIFAR-10)

## The Future: Convergence
- **Code models become agents**: Qwen2.5-Coder-32B + function calling → coding agent
- **Agents drive model training**: SWE-agent trajectories used to train specialized code models
- **Reasoning models for code**: [[sources/llama-nemotron|Llama-Nemotron]], [[sources/deepseek-r1|DeepSeek-R1]] apply reasoning to code
- **Real-time coding**: Cursor, Copilot integrate models into IDEs for real-time assistance
- **GPU kernel generation**: LLMs generating high-performance compute kernels (KernelBench-X frontier)
- **Domain-specific tool agents**: Biomedical, legal, scientific tool-calling datasets for specialized agents

## Key Papers
- [[sources/starcoder]] — StarCoder: Open code LLM standard
- [[sources/starcoder-2]] — StarCoder 2: Next generation with The Stack v2
- [[sources/code-llama]] — Code Llama: Meta's code-specialized Llama
- [[sources/qwen25-coder]] — Qwen2.5-Coder: Current SOTA code models
- [[sources/swe-agent]] — SWE-agent: First effective coding agent
- [[sources/codeact]] — CodeAct: Code as agent actions
- [[sources/llama-nemotron]] — Llama-Nemotron: Reasoning for code
- [[sources/kernelbenchx]] — KernelBench-X: Benchmarking LLM-generated GPU kernels
- [[sources/biotool-medical]] — BioTool: Biomedical tool-calling for specialized agents
- [[sources/dci-agent-retrieval]] — DCI Agent: Direct corpus interaction for agentic search
- [[sources/swe-webdevbench]] — SWE-WebDevBench: Evaluating AI platforms as software agencies
- [[sources/auto-research-agents]] — Auto Research: Specialist agents develop training recipes

## See Also
- [[entities/models/starcoder]] — StarCoder model family
- [[entities/datasets/the-stack]] — The Stack training data
- [[concepts/agents]] — LLM Agents & Tool Use
- [[comparisons/open-model-families]] — Open model family comparison
