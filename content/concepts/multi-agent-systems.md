---
type: concept
tags: [agents, multi-agent, reasoning, inference, 2024]
---

# Multi-Agent LLM Systems

> Using multiple LLMs in coordinated architectures — either at inference time (MoA, debate) or through joint training (MALT) — to exceed single-model capabilities.

## Overview
Multi-agent LLM systems arrange multiple language models in collaborative architectures where each model plays a specialized role or iteratively refines outputs. This approach exploits a key finding: LLMs generate better responses when given reference outputs from other models (the "collaborativeness" property).

Two main paradigms have emerged:
1. **Inference-time multi-agent** (no training): Orchestrate existing models in layers or debate rounds
2. **Training-time multi-agent** (jointly trained): Train specialized models to collaborate on tasks

## How It Works

### Inference-Time: Mixture-of-Agents (MoA)
[[sources/mixture-of-agents|Mixture-of-Agents]] arranges LLMs in layers:
- **Layer 1**: Multiple "proposer" LLMs generate diverse initial responses
- **Layer 2+**: "Aggregator" LLMs see previous layer outputs and produce refined responses
- **Final layer**: Single aggregator synthesizes the best answer

Result: Open-source LLMs collectively surpass GPT-4o on AlpacaEval 2.0 (65.1% vs 57.5%).

### Training-Time: MALT
[[sources/malt|MALT]] trains three specialized LLMs:
- **Generator**: Produces initial solutions
- **Verifier**: Checks correctness
- **Refiner**: Improves wrong answers

Joint reward signals incentivize cooperation. Result: ~15% improvement on MATH over single-model baselines.

### Multi-Agent Debate
Multiple LLMs debate and critique each other's responses over multiple rounds, converging to higher-quality answers through iterative refinement.

### Hierarchical Research Agents: AI Co-Mathematician

[[sources/ai-co-mathematician|AI Co-Mathematician (2026)]] demonstrates multi-agent systems for **open-ended mathematical research**:

- **Project Coordinator**: Top-level agent managing user interaction and high-level research direction
- **Workstream Coordinators**: Independent agents tackling parallel research goals (literature review, computational experiments, proof attempts)
- **Specialized Sub-Agents**: Literature search, coding (persistent file system), Gemini Deep Think (theorem proving)
- **Reviewer Agents**: Iteratively verify and critique workstream outputs via review cycles

Key innovations:
- **Asynchronous execution**: Agents work in parallel without blocking each other or the user
- **Internal messaging system**: Structured communication between agent hierarchy levels
- **Progressive disclosure**: User sees high-level coordinator summaries; can drill into workstream details
- **Failed exploration preservation**: Dead ends are first-class permanent records, not discarded

Result: **48% on FrontierMath Tier 4** (SOTA) — hierarchical multi-agent organization significantly outperforms single-model baselines (19% for Gemini 3.1 Pro alone).

## Key Papers
- [[sources/mixture-of-agents|Mixture-of-Agents]] (2024) — Inference-time MoA, SOTA on AlpacaEval 2.0
- [[sources/malt|MALT]] (2024) — Training-time multi-agent, ~15% gain on MATH
- [[sources/react|ReAct]] (2022) — Single-agent foundation
- [[sources/codeact|CodeAct]] (2024) — Code as agent actions
- [[sources/ai-co-mathematician|AI Co-Mathematician]] (2026) — Hierarchical research agents for mathematics, 48% FrontierMath Tier 4

## Comparison with Related Approaches

| Approach | Training Required | Models | Key Advantage |
|---|---|---|---|
| Single-model (CoT) | No | 1 | Simple, fast |
| Self-refinement | No | 1 | No extra models |
| MoA (inference) | No | N (any) | Leverages diverse models |
| MALT (training) | Yes | 3 specialized | Models learn to cooperate |
| Multi-agent debate | No | N (same or different) | Iterative improvement |
| AI Co-Mathematician | No | Hierarchical (coordinator + workstreams + reviewers) | Asynchronous research with hard verification |

## See Also
- [[concepts/agents|LLM Agents & Tool Use]] — single-agent paradigm
- [[concepts/mixture-of-experts|Mixture of Experts]] — parameter-level routing (different concept)
- [[concepts/chain-of-thought|Chain-of-Thought]] — single-model reasoning
- [[concepts/test-time-compute|Test-Time Compute Scaling]] — compute at inference time
