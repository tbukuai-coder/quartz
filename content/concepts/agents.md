---
type: concept
tags: [agents, tool-use, reasoning, agentic-rl]
---

# LLM Agents & Tool Use

> Enabling LLMs to **interact with external tools and environments** by interleaving reasoning with actions — the foundation of autonomous AI systems that can search, code, browse, and accomplish real-world tasks.

## Overview
LLM agents extend language models beyond text generation into **action execution**. Rather than just producing text answers, agents can call APIs, execute code, browse the web, and interact with software — all while maintaining an internal reasoning process that guides their actions.

## How It Works

### The ReAct Loop
The foundational agent paradigm ([[sources/react|ReAct]], 2022):
```
Thought: I need to find X to answer this question
Action: Search["X"]
Observation: [search results about X]
Thought: Based on the results, I can now determine...
Action: Finish["answer"]
```

Reasoning traces ("Thoughts") help the agent:
- Decompose complex tasks into subtasks
- Plan which actions to take next
- Handle unexpected observations
- Recover from errors

### Action Representations

| Format | Pros | Cons | Example |
|---|---|---|---|
| **Text** | Simple | Limited expressiveness | `Search[query]` |
| **JSON** | Structured, parseable | No composition, no control flow | `{"tool": "search", "args": {...}}` |
| **Code** ([[sources/codeact|CodeAct]]) | Composition, debugging, libraries | Requires interpreter | `result = search(query); df = pd.DataFrame(result)` |

### CodeAct: Code as Actions
[[sources/codeact|CodeAct]] (2024) demonstrated that using **executable Python code** as the action format is strictly superior:
- **Compose** multiple tool calls: `tool_a(tool_b(x))`
- **Control flow**: loops, conditionals, error handling
- **Self-debugging**: read tracebacks, fix code, retry
- **Library access**: use pandas, numpy, sklearn, etc.
- Adopted by Hugging Face's **smolagents** library

### Structured Generation for Agents
[[concepts/structured-generation|Structured generation]] is critical for reliable agents:
- Tool calls must produce valid JSON/function signatures — [[sources/outlines|Outlines]] guarantees this via FSM-based decoding
- [[sources/sglang|SGLang]]'s compressed FSM enables structured outputs with minimal overhead
- Without structured generation, agents fail on malformed tool calls

## Key Capabilities
1. **Tool use**: Call APIs, search engines, calculators, code interpreters
2. **Multi-step reasoning**: Plan and execute complex task sequences
3. **Self-correction**: Detect and recover from errors via observation feedback
4. **Memory**: Maintain context across interaction turns
5. **Collaboration**: Communicate with humans and other agents

## Agentic RL: Reinforcement Learning for Agents

A rapidly growing subfield applies RL to improve agents' reasoning and tool-use capabilities. [[sources/agentic-rl-reasoning|Yu et al. (2025)]] provide a comprehensive investigation with key findings:

### Key Insights from Agentic RL Research
1. **Real trajectories > synthetic data**: End-to-end tool-use trajectories from actual agent interactions produce far stronger SFT initialization than stitched/synthetic data — synthetic trajectories miss critical decision points at tool invocation boundaries
2. **Deliberative strategy wins**: Fewer but more thoughtful tool calls outperform both frequent-tool-call and verbose self-reasoning approaches — quality of tool use matters more than quantity
3. **Exploration-friendly techniques are essential**: Clip-higher, overlong reward shaping, and policy entropy management are critical for agentic RL training (GRPO-TCR recipe)
4. **Model-aware data curation**: RL training data should be filtered based on the specific model's capability — questions too easy or too hard waste training signal
5. **Small models can compete**: With proper recipes, 4B models surpass 32B models in agentic reasoning

### Multi-Turn Credit Assignment
[[sources/multi-turn-agent-rl|Zeng et al. (2025)]] identified a critical problem: standard RL algorithms treat multi-turn agent trajectories as single-turn bandit problems, collapsing all turn-level signals into a sparse trajectory-level reward. They proposed:

- **MT-GRPO**: Multi-turn GRPO with turn-level advantages computed per interaction turn
- **MT-PPO**: Multi-turn PPO with critic-based value estimation — more scalable for long horizons
- **Turn-level rewards**: Retrieval quality per search turn, format correctness per tool call, answer correctness at trajectory end

Key result: MT-PPO achieves near-perfect format correctness (99.9%) and substantially more stable training than trajectory-level baselines, with faster convergence in the first 100 steps.

### Agentic RL vs Standard RL for Reasoning
| Aspect | Standard RLVR | Agentic RL |
|---|---|---|
| **Environment** | Single-turn, no tools | Multi-turn, code interpreter |
| **Actions** | Generate text | Reason + call tools + verify |
| **Data** | Math/code problems | Diverse + end-to-end trajectories |
| **Key challenge** | Reward design | Trajectory quality + entropy + credit assignment |
| **Best strategy** | Outcome rewards | Deliberative tool use + turn-level rewards |

## Open Multimodal Search Agents: OpenSearch-VL

[[sources/opensearch-vl|OpenSearch-VL (2026)]] provides the first **fully open recipe** for training frontier multimodal deep search agents:

### Three Open Components
1. **Data**: 36K SFT + 8K RL trajectories from Wikipedia multi-hop VQA pipeline with fuzzy entity rewriting and source-anchor visual grounding
2. **Tools**: Beyond search — OCR, cropping, sharpening, super-resolution, perspective correction for real-world visual imperfections
3. **Training**: Fatal-aware Multi-Turn GRPO with composite reward (format + accuracy + query quality)

### Fatal-Aware RL
- **Fatal step index**: Earliest step with K=3 consecutive tool-execution errors
- **Token masking**: Zeros out all tokens after fatal step — preserves valid pre-failure reasoning, discards noisy post-failure gradients
- **One-sided advantage clamping**: Preserves useful pre-failure reasoning while preventing suppression of viable early steps

### Results
- OpenSearch-VL-32B: **63.7 average** across 7 benchmarks (SimpleVQA, VDR, MMSearch, LiveVQA, BrowseComp-VL, FVQA, InfoSeek)
- Outperforms proprietary models: Gemini-2.5-Pro (46.0), GPT-5 (45.1)
- Scales from 8B (56.6 avg) to 30B-A3B (61.6) to 32B (63.7)

## Unified Skill Evolution: Skill1

[[sources/skill1|Skill1 (2026)]] achieves unified evolution of all three stages of the skill-augmented agent lifecycle:

### The Three Stages (All Jointly Optimized)
1. **Skill Selection**: Generate query → retrieve candidates → re-rank via policy → select best skill
2. **Skill Utilization**: Multi-turn environment interaction conditioned on selected skill
3. **Skill Distillation**: Reflect on trajectory → produce reusable strategy + scenario description → admit to library on success

### Shared Task-Outcome Credit Assignment
- **Utilization**: Direct outcome $R_i^{\text{util}} = r(\tau_i)$
- **Selection**: NDCG-based re-ranking reward against per-skill utility trends (EMA of outcomes across episodes)
- **Distillation**: $R_i^{\text{distill}} = r(\tau_i) - \hat{U}_i$ — is this experience better than what we already know?

### Results
- ALFWorld: **97.5%** average success (+2.6 over RetroAgent)
- WebShop: **82.9%** success
- Ablations: Removing library entirely drops -16.6 points; removing any credit signal degrades all capabilities

## Skill Curation for Self-Evolving Agents: SkillOS

[[sources/skillos|SkillOS (2026)]] addresses the critical gap of **skill curation** — how agents should manage, update, and prune their skill collections over time for long-term proficiency in streaming settings:

### System Architecture
- **SkillRepo**: External Markdown-based skill collection (YAML frontmatter + instructions)
- **Agent Executor (π_L)**: Frozen LLM that retrieves skills via BM25 and solves tasks
- **Skill Curator (π_S)**: Trainable model that observes trajectories and generates curation operations (`insert_skill`, `update_skill`, `delete_skill`)

### Two Core Training Designs
1. **Task Groups for Long-Term Utility**: Training instances are groups of related tasks — skills from earlier experiences are evaluated by their ability to improve later tasks
2. **Composite Reward**: Task performance + valid function calls + skill quality + SkillRepo compactness

### Results
- ALFWorld: **62.8%** average success (+7.1 over SkillOS-base, +9.8% relative over ReasoningBank)
- **−6.0% fewer interaction steps** vs strongest baseline
- 8B curator **outperforms Gemini-2.5-Pro** when used as curator
- Generalizes across executors (Qwen3-8B → Gemini-2.5-Pro) and task domains
- Skills evolve into richly structured Markdown encoding higher-level meta-skills over time

## Scientific AI Agents: Heterogeneous Foundation Model Collaboration

A new frontier extends agentic systems beyond language-centric LLMs to **heterogeneous scientific foundation models** that operate over non-linguistic data modalities (symbolic formulas, time series, molecular structures). [[sources/eywa|Eywa (2026)]] introduces a three-stage framework inspired by Avatar's Tsaheylu (neural bond for cross-species communication):

### The Eywa Framework
1. **EywaAgent**: Augments domain-specific foundation models (for scientific data types) with an FM-LLM language interface, enabling language agents to guide inference and planning over specialized tasks
2. **EywaMAS**: Multi-agent extension where EywaAgents collaborate with conventional LLM agents in multi-agent systems
3. **EywaOrchestra**: Planning-based orchestration dynamically coordinating both language agents and EywaAgents via a central planner

**Key result**: EywaAgent improves utility by ~7% across physical, life, and social science tasks while reducing token usage by ~30% and execution time by ~10%.

This direction is critical as scientific AI increasingly depends on domain-specific foundation models that do not natively support language I/O — the Tsaheylu interface bridges this gap without requiring full modality translation into natural language.

## AI-Assisted Mathematics: The AI Co-Mathematician

[[sources/ai-co-mathematician|AI Co-Mathematician (2026)]] represents a new paradigm in scientific AI agents: an **interactive, asynchronous workbench** that coordinates hierarchical AI agents to support open-ended mathematical research:

### Hierarchical Agent Architecture
- **Project Coordinator**: Top-level agent managing user interaction and research direction
- **Workstream Coordinators**: Parallel agents tackling independent goals (literature review, computational experiments, proof attempts)
- **Specialized Sub-Agents**: Literature search, coding, Gemini Deep Think (theorem proving), reviewer agents
- **Reviewer Agents**: Enforce correctness through iterative review cycles with hard programmatic constraints

### Seven Design Principles
1. Embrace mathematics beyond proofs (ideation, computation, literature)
2. Support iterative refinement of intent (dialogue before solving)
3. Produce native mathematical artifacts (living working papers with margin notes)
4. Enable asynchronous interaction and flexible steering
5. Manage cognitive load via progressive disclosure
6. Track, manage, and communicate uncertainty
7. Preserve the history of failed explorations

### Results
- **48% on FrontierMath Tier 4** (SOTA among all AI systems) — from 19% base Gemini 3.1 Pro
- Solved open Kourovka Notebook Problem 21.10 (with human collaboration)
- Key insight: **bidirectional human-AI collaboration** was essential — AI found strategies humans couldn't, humans filled gaps AI couldn't

This represents the mathematics-specific instantiation of the broader scientific agent paradigm established by [[sources/eywa|Eywa]] and [[sources/intern-atlas|Intern-Atlas]].

## Agent-Native Research Artifacts (Ara)

As AI agents become primary consumers of scientific knowledge, the current PDF publication format imposes two structural costs:

1. **Storytelling Tax**: Narrative compilation erases failed experiments, rejected hypotheses, and branching exploration trajectories — knowledge that agents need to avoid rediscovering dead ends (failed runs account for 90.2% of total agent cost in METR benchmarks)
2. **Engineering Tax**: Paper-level documentation is sufficient for human reviewers but insufficient for agent execution — only 45.4% of PaperBench reproduction requirements are fully specified

[[sources/agent-native-research-artifact|Ara (2026)]] proposes a four-layer protocol recasting the primary research object from narrative document to agent-executable knowledge package:
- **Structured scientific logic**: Queryable claims and dependency graphs
- **Executable code**: Full operational specifications (not just reviewer-sufficient descriptions)
- **Exploration graph**: Preserved branching research process — failures, pivots, design choices
- **Grounded evidence**: Every claim bound to raw empirical outputs

## Bi-Level Multi-Agent Web Search: Web2BigTable

[[sources/web2bigtable|Web2BigTable (2026)]] extends the agent paradigm to internet-scale information extraction with a bi-level multi-agent architecture for web-to-table search, achieving 7.5× better Avg@4 Success Rate than SOTA. The system uses a closed-loop run-verify-reflect pattern where multiple agents collaboratively search, verify, and refine table extractions from web sources.

## Direct Corpus Interaction: Beyond Semantic Retrieval

[[sources/dci-agent-retrieval|DCI Agent (2026)]] challenges the fundamental agent-retrieval paradigm. Current agents call retriever APIs that return top-k documents, but this compresses corpus access into a single similarity-matching step that fails for:
- Exact lexical constraints
- Sparse clue conjunctions
- Local context checks
- Multi-step hypothesis refinement

**Direct Corpus Interaction (DCI)** gives agents terminal-style access to raw text: grep-like searches, document browsing, pattern matching, iterative exploration. The agent uses its reasoning to navigate the corpus rather than relying on pre-computed similarity scores. Evaluated on BEIR datasets, BrowseComp-Plus, and multi-hop QA, DCI outperforms traditional retrieval on complex agentic search tasks.

## Biomedical Tool-Calling: BioTool

[[sources/biotool-medical|BioTool (2026)]] demonstrates that domain-specific tool-calling is essential for specialized agent performance. While general tool-calling datasets improve generic agent capabilities, LLMs perform poorly on biomedical tasks because they cannot leverage the tools clinical experts use daily (NCBI, Ensembl, UniProt).

BioTool provides a comprehensive biomedical tool-calling dataset covering genomics, proteomics, and evolution research APIs. Fine-tuned models outperform commercial biomedical LLM tools, showing that **domain-specific tool datasets are as important as general tool-calling datasets** for specialized agent deployment.

## Agentic Turn-Level Credit Assignment: A²TGPO

[[sources/a2tgpo-agentic|A²TGPO (2026)]] addresses a critical gap in agentic RL: standard GRPO treats multi-turn agent trajectories as single-turn bandit problems, collapsing all turn-level signals into a sparse trajectory-level reward. This makes it impossible to evaluate which specific tool call contributed to success or failure.

**A²TGPO** (Agentic Turn-Group Policy Optimization) introduces:
- **Turn-level grouping**: Groups rollout samples by turn rather than full trajectory
- **Information gain normalization**: Measures how much each tool call contributes
- **Variance-rescaled discounted accumulation**: Adjusts updates based on per-turn reward variance
- **Adaptive turn-level clipping**: ε threshold adapts per-turn based on turn-level statistics

This enables proper credit assignment across multi-turn interactions without requiring external process reward models or constraining trajectory diversity.

## World Action Models in Robotics

[[sources/trust-imagination-wam|When to Trust Imagination (2026)]] addresses a critical problem in robotic agents using World Action Models (WAMs):
- Current WAMs execute a fixed number of predicted actions after each inference, blind to whether the imagined future remains consistent with reality
- The paper formulates **adaptive WAM execution** as future-reality verification: execute actions only while the predicted and actual states match
- When divergence exceeds threshold, stop and re-query the WAM with updated state
- This prevents compounding errors from blindly following outdated predictions, achieving 0.95 success rate on long-horizon manipulation tasks

## Creative Tool Use: CreativityBench

[[sources/creativitybench|CreativityBench (2026)]] reveals a fundamental gap in current agent evaluation: **reasoning ability does not imply creative intelligence**. The benchmark evaluates affordance-based creative tool use — repurposing objects based on fine-grained physical attributes rather than semantic plausibility:

- **14K tasks** reverse-engineered from a 157K-affordance knowledge base (4K entities, 26K parts)
- Models achieve **51.5% entity correctness** but only **19.1% gold correctness** (correct entity + correct part) — a >60% drop
- **Qwen3-32B outperforms GPT-5.2** in creative discovery despite weaker general reasoning — showing dissociation between reasoning and creativity
- Performance **saturates with model size** and is bounded by affordance commonality — rare tool repurposing remains extremely difficult
- Standard interventions (temperature, CoT, interactive evaluation) yield **minimal gains** — creative reasoning requires fundamentally different training signals

## Evolution
| Year | Development | Paper |
|---|---|---|
| 2022 | ReAct loop (Thought-Action-Observation) | [[sources/react]] |
| 2023 | Tool-augmented LLMs (Llama 3 tool training) | [[sources/llama-3]] |
| 2023 | Guaranteed structured outputs (Outlines FSM) | [[sources/outlines]] |
| 2024 | Code as actions (CodeAct → smolagents) | [[sources/codeact]] |
| 2024 | Agent fine-tuning datasets (CodeActInstruct) | [[sources/codeact]] |
| 2024–25 | Agent benchmarks in model evals (BFCL in Qwen3) | [[sources/qwen3]] |
| 2025 | **Agentic RL**: RL for tool-using agents | [[sources/agentic-rl-reasoning]] |
| 2025 | **Turn-level credit assignment**: MT-GRPO/MT-PPO for multi-turn agents | [[sources/multi-turn-agent-rl]] |
| 2026 | **Heterogeneous scientific agents**: Eywa framework for non-linguistic FMs | [[sources/eywa]] |
| 2026 | **Agent-native research artifacts**: Ara protocol replacing PDFs | [[sources/agent-native-research-artifact]] |
| 2026 | **Methodological evolution graphs**: Intern-Atlas for AI-driven discovery | [[sources/intern-atlas]] |
| 2026 | **Bi-level web search agents**: Web2BigTable for internet-scale extraction | [[sources/web2bigtable]] |
| 2026 | **Direct corpus interaction**: DCI for agentic retrieval beyond similarity | [[sources/dci-agent-retrieval]] |
| 2026 | **Biomedical tool-calling**: BioTool for specialized domain agents | [[sources/biotool-medical]] |
| 2026 | **Turn-level agentic credit**: A²TGPO for multi-turn tool-use RL | [[sources/a2tgpo-agentic]] |
| 2026 | **Adaptive WAM execution**: When to Trust Imagination for robotics | [[sources/trust-imagination-wam]] |
| 2026 | **Open multimodal search agents**: OpenSearch-VL with fatal-aware GRPO | [[sources/opensearch-vl]] |
| 2026 | **Unified skill evolution**: Skill1 co-evolves selection, utilization, distillation | [[sources/skill1]] |
| 2026 | **Skill curation**: SkillOS learns to manage skill collections via RL | [[sources/skillos]] |
| 2026 | **Creative tool use**: CreativityBench reveals reasoning ≠ creativity | [[sources/creativitybench]] |
| 2026 | **AI-assisted mathematics**: AI Co-Mathematician — hierarchical agent workbench for math research | [[sources/ai-co-mathematician]] |

## Key Papers
- [[sources/react]] — ReAct: The foundational agent paradigm (2000+ citations)
- [[sources/codeact]] — CodeAct: Code actions, adopted by smolagents
- [[sources/outlines]] — Outlines: Guaranteed structured outputs for tool calls
- [[sources/llama-3]] — Tool-use training in Llama 3's post-training
- [[sources/agentic-rl-reasoning]] — Demystifying RL in Agentic Reasoning: recipes for tool-use RL
- [[sources/multi-turn-agent-rl]] — Turn-level credit assignment for multi-turn agent RL
- [[sources/eywa]] — Eywa: Heterogeneous agentic framework for scientific foundation models
- [[sources/agent-native-research-artifact]] — Ara: Agent-native research artifacts replacing PDFs
- [[sources/intern-atlas]] — Intern-Atlas: Methodological evolution graphs for AI scientists
- [[sources/web2bigtable]] — Web2BigTable: Bi-level multi-agent web-to-table search
- [[sources/dci-agent-retrieval]] — DCI Agent: Direct corpus interaction for agentic search
- [[sources/biotool-medical]] — BioTool: Biomedical tool-calling dataset for domain agents
- [[sources/a2tgpo-agentic]] — A²TGPO: Agentic turn-group policy optimization
- [[sources/trust-imagination-wam]] — When to Trust Imagination: Adaptive WAM execution for robotics
- [[sources/opensearch-vl]] — OpenSearch-VL: Open recipe for multimodal search agents
- [[sources/skill1]] — Skill1: Unified evolution of skill-augmented agents
- [[sources/skillos]] — SkillOS: Learning skill curation for self-evolving agents
- [[sources/creativitybench]] — CreativityBench: Evaluating creative tool use in agents
- [[sources/claw-eval-live]] — Claw-Eval-Live: Live benchmark for workflow agents
- [[sources/ai-co-mathematician]] — AI Co-Mathematician: Hierarchical agent workbench for mathematics research

## See Also
- [[concepts/structured-generation]] — Guaranteeing valid tool-call outputs
- [[concepts/rag]] — Retrieval-augmented generation (a specific form of tool use)
- [[concepts/rlhf]] — Alignment for agent safety
- [[comparisons/rl-reasoning-methods]] — RL methods comparison including agentic approaches
- [[concepts/multi-agent-systems]] — Multi-agent coordination and collaboration
