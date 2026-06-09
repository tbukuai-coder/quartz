---
type: source
arxiv_id: "2210.03629"
title: "ReAct: Synergizing Reasoning and Acting in Language Models"
authors: ["Shunyu Yao", "Jeffrey Zhao", "Dian Yu", "Nan Du", "Izhak Shafran", "Karthik Narasimhan", "Yuan Cao"]
date: 2022-10-06
org: "Google Brain / Princeton"
tags: [agents, reasoning, tool-use, foundational, 2022]
upvotes: 34
---

# ReAct: Synergizing Reasoning and Acting in Language Models

> The **foundational paper for LLM agents**. Introduces the **Thought → Action → Observation** loop that interleaves reasoning traces with task-specific actions, enabling LLMs to interact with external tools and environments while maintaining interpretable decision-making.

## Key Contributions
- **ReAct paradigm**: Interleave reasoning traces ("Thought") with environment actions ("Action") and feedback ("Observation") in a unified generation loop
- Showed that reasoning + acting is **synergistic**: reasoning helps guide actions, while actions ground reasoning in real-world observations
- **Dramatically outperforms** pure chain-of-thought (no action) and pure action (no reasoning) approaches
- Established the template used by virtually all subsequent agent frameworks (LangChain, LlamaIndex, smolagents, AutoGPT)
- Few-shot prompting only — no fine-tuning needed (2–6 examples)
- 2000+ citations, most influential agent paper

## Method
### The ReAct Loop
At each step, the LLM generates:
1. **Thought** (optional): Internal reasoning — decompose the task, form hypotheses, plan next steps
2. **Action**: An executable action (e.g., `Search[query]`, `Lookup[term]`, `Finish[answer]`)
3. **Observation**: Environment returns the result of the action

The model alternates between thinking and acting, building up context through the trajectory. Key properties:
- Thoughts provide **interpretable** reasoning traces (unlike pure RL agents)
- Actions **ground** the reasoning in real information (unlike pure CoT which hallucinates)
- The interleaved format allows **dynamic replanning** when observations contradict expectations

### Tasks and APIs
- **HotpotQA** (multi-hop QA): Wikipedia Search/Lookup API — requires finding and combining info from multiple pages
- **FEVER** (fact verification): Same Wikipedia API — verify claims as supported/refuted
- **ALFWorld** (interactive text game): Household task actions (go to, take, clean, put)
- **WebShop** (web shopping): Search, click, buy actions

### Prompting
- Few-shot: 6 examples for HotpotQA, 3 for FEVER, 1–2 for decision tasks
- Each example shows the full Thought-Action-Observation trajectory
- No fine-tuning required — works with PaLM-540B and GPT-3

## Results
- **HotpotQA**: ReAct (PaLM-540B) achieves 35.1% improvement over CoT-only on multi-hop QA
- **FEVER**: ReAct achieves higher accuracy than CoT by grounding in actual Wikipedia lookups
- **ALFWorld**: 34% absolute improvement over imitation learning baselines
- **WebShop**: 10% improvement over RL methods, with only 1–2 in-context examples
- **ReAct + CoT-SC** (self-consistency): Best of both worlds — use CoT-SC for internal reasoning, fall back to ReAct when confidence is low

### Fine-tuning Results
- Fine-tuned PaLM-8B/62B with ReAct trajectories outperform much larger prompted models
- ReAct fine-tuning benefits from action grounding more than CoT fine-tuning

## Connections
- **Influenced**: [[sources/codeact]] (CodeAct — actions as code, used in smolagents), virtually all agent frameworks
- **Builds on**: Chain-of-Thought prompting (Wei et al., 2022), tool-augmented LMs
- **Key concepts**: [[concepts/agents]], [[concepts/tool-use]]
- **Organizations**: [[entities/orgs/google]]

## Citation
> Yao et al., "ReAct: Synergizing Reasoning and Acting in Language Models," ICLR 2023, arXiv:2210.03629, 2022.
> https://huggingface.co/papers/2210.03629
