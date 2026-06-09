---
type: source
arxiv_id: "2605.06651"
title: "AI Co-Mathematician: Accelerating Mathematicians with Agentic AI"
authors: ["Daniel Zheng", "Ingrid von Glehn", "Yori Zwols", "Iuliya Beloshapka", "Lars Buesing", "Daniel M. Roy", "Martin Wattenberg", "Bogdan Georgiev", "Tatiana Schmidt", "Andrew Cowie"]
venue: "arXiv preprint"
year: 2026
date: "2026-05"
org: "Google DeepMind"
upvotes: 5
tags: [agents, mathematics, scientific-ai, agentic-reasoning, multi-agent-systems, theorem-proving]
github: null
---

# AI Co-Mathematician: Accelerating Mathematicians with Agentic AI

> An interactive, asynchronous **agentic workbench** for professional mathematicians that coordinates hierarchical AI agents to support open-ended research — including ideation, literature search, computational exploration, theorem proving, and theory building — achieving **48% on FrontierMath Tier 4** (new SOTA among all AI systems).

## Key Contributions

1. **Interactive agentic workbench for mathematics**: Not a chatbot but an asynchronous, stateful workspace with hierarchical agent organization (project coordinator → workstream coordinators → specialized sub-agents) that mirrors human collaborative research workflows
2. **Seven design principles for AI-assisted mathematics**: Embrace beyond-proofs activities, iterative intent refinement, native mathematical artifacts (living working papers), asynchronous flexible steering, progressive disclosure, uncertainty management, and preservation of failed explorations
3. **Hard programmatic constraints**: Reviewer agents enforce correctness via iterative review cycles with margin annotations — preventing invalid shortcuts, hallucinated lemmas, and premature claims
4. **Real mathematical discoveries**: Solved an open Kourovka Notebook problem (Problem 21.10), proved conjectures on Stirling coefficients, and found lemmas in Hamiltonian systems — all by professional mathematicians using the tool independently
5. **SOTA on FrontierMath Tier 4**: 48% accuracy (23/48 problems) on Epoch AI's hardest benchmark tier ("short-term research projects by professors"), including 3 problems unsolved by any prior system — a significant jump from base Gemini 3.1 Pro at 19%

## Method

### Agent Hierarchy

```
User ←→ Project Coordinator Agent
              ├── Workstream Coordinator (Goal 1)
              │     ├── Literature Search Sub-Agent
              │     ├── Coding Sub-Agent
              │     └── Gemini Deep Think Sub-Agent
              ├── Workstream Coordinator (Goal 2)
              │     ├── ...
              └── Workstream Coordinator (Goal N)
                    └── Reviewer Agents (iterative review cycles)
```

**Communication**: Internal messaging system allows parallel asynchronous work; user talks only to project coordinator (progressive disclosure); can drill into any workstream on demand.

### The Research Workflow

1. **Intent Refinement**: Project coordinator opens dialogue to clarify and formalize the research question — no immediate solving
2. **Goal Definition**: User approves formalized goals; coordinator creates parallel workstreams
3. **Branching Execution**: Each workstream coordinator runs independently — literature review, computational experiments, proof attempts, coding — producing incremental reports
4. **Hard Constraints via Review**: Specialized reviewer agents continuously check workstream outputs; flawed arguments are flagged and sent back for revision
5. **Living Working Paper**: Final output is a structured document with inline provenance, margin annotations marking uncertainty/contentiousness, and links to evidence — not transient chat
6. **Failed Exploration Preservation**: Dead ends are permanently recorded as first-class outcomes, informing future workstreams

### Key Design Principles

| Principle | Implementation |
|---|---|
| **Embrace beyond proofs** | Literature search, computational experiments, conjecture formulation — not just theorem proving |
| **Iterative intent refinement** | Onboarding dialogue before any work begins; goals formalized collaboratively |
| **Native mathematical artifacts** | Living working papers with margin notes, not chat logs |
| **Asynchronous interaction** | Multiple agents work in parallel; user can interrupt/steer at any time |
| **Progressive disclosure** | User sees project coordinator summaries by default; can drill into agent details |
| **Uncertainty management** | Version history, numerical simulations, citation checking; margin highlights for uncertain claims |
| **Preserve failed explorations** | Dead ends are permanent records — knowing what doesn't work is essential |

### Specialized Capabilities
- **Literature search tools**: Computationally intensive retrieval + direct web/paper access for exact theorem statements
- **Coding agents**: Persistent file system for developing complex libraries, SAT solvers, numerical simulations
- **Gemini Deep Think integration**: For difficult proof sub-tasks
- **Reviewer agents**: Iterative review cycles with specific error identification

## Results

### FrontierMath Tier 4 (Epoch AI — blind evaluation)
| System | Accuracy | Problems Solved |
|---|---|---|
| Gemini 3.1 Pro (base) | 19% | ~9/48 |
| **AI Co-Mathematician** | **48%** | **23/48** |

- Blind evaluation: Epoch AI entered problems and retrieved answers without developer observation
- **3 problems solved** that no prior AI system had solved
- Time budget: 48 hours per problem (most finish well within)
- Significant compute: comparable to a long AI-assisted software engineering session

### Internal Research Mathematics Benchmark (100 problems)
- Significantly outperforms single-call Gemini 3.1 Pro and Gemini 3.1 Deep Think
- Advantages from: persistent file system (SAT solvers, complex libraries), literature access (exact theorem retrieval), iterative review (error correction over multiple passes)

### Case Studies with Professional Mathematicians

| User | Domain | Outcome |
|---|---|---|
| M. Lackenby | Topology / Group Theory | **Solved open Kourovka Notebook Problem 21.10** — AI found clever but flawed strategy; human filled gap; bidirectional collaboration |
| G. Bérczi | Representation Theory | **Proved conjectures on Stirling coefficients** — system found inductive formula where AlphaEvolve failed; margin notes flagged key insight |
| S. Rezchikov | Hamiltonian Systems | **Proved a technical lemma** — other AI systems failed; system's persistent exploration succeeded |

### Key Insight: Human-in-the-Loop is Essential
Lackenby: "The system works best when the user is familiar with the area." The AI found a strategy the human couldn't, and the human filled a gap the AI couldn't — **bidirectional collaboration** was key.

## Challenges & Limitations

1. **Reviewer-Pleasing Bias (False Consensus)**: Flawed arguments can converge to satisfy reviewer agents while remaining incorrect — hard for humans to detect
2. **Intractable Disagreements (Death Spirals)**: Review cycles can fail to terminate, degrading into hallucinated reasoning loops
3. **Autonomy vs Control**: Long-running autonomous exploration can hit unplanned difficulties; current models' judgment on what to do is far behind humans
4. **Semantic Meaning of Representations**: Polished LaTeX creates false confidence — well-typeset ≠ rigorous
5. **Signal-to-Noise in Literature**: Risks flooding community with plausible but shallow/flawed papers
6. **Peer Review Burden**: AI generates 20-page proofs in minutes; human verification takes days — asymmetric scaling

## Connections

- [[sources/eywa|Eywa]] — Heterogeneous scientific agent framework; AI Co-Mathematician is the mathematics-specific instantiation of the broader scientific AI agent paradigm
- [[sources/intern-atlas|Intern-Atlas]] — Methodological evolution graphs for AI scientists; complementary approach to accelerating research
- [[sources/agent-native-research-artifact|Ara]] — Agent-native research artifacts protocol; AI Co-Mathematician produces native mathematical artifacts aligning with Ara's vision
- [[sources/deepseek-prover-v2|DeepSeek-Prover-V2]] — Formal theorem proving via RL; AI Co-Mathematician uses informal proving with reviewer-based verification instead
- [[concepts/agents|LLM Agents]] — Instantiates hierarchical multi-agent architecture with domain-specific specialization
- [[concepts/multi-agent-systems|Multi-Agent Systems]] — Project coordinator + workstream coordinators + reviewer agents as structured multi-agent collaboration
- [[entities/orgs/google|Google DeepMind]] — Developed at Google DeepMind, building on Gemini 3.1 Pro
- [[comparisons/code-models-agents|Code Models & Agents]] — Includes coding agents for computational mathematics
