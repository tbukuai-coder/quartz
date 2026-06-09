---
type: source
arxiv_id: "2402.01030"
title: "Executable Code Actions Elicit Better LLM Agents"
authors: ["Xingyao Wang", "Yangyi Chen", "Lifan Yuan", "Yizhe Zhang", "Yunzhu Li", "Hao Peng", "Heng Ji"]
date: 2024-02-01
org: "UIUC"
tags: [agents, tool-use, code-generation, 2024]
upvotes: 192
---

# CodeAct: Executable Code Actions Elicit Better LLM Agents

> Proposes using **executable Python code as the unified action space** for LLM agents — enabling tool composition, dynamic revision, and self-debugging via a Python interpreter. Directly inspired the design of Hugging Face's **smolagents** library.

## Key Contributions
- **CodeAct**: Replace JSON/text action formats with executable Python code — agents write and execute code to accomplish tasks
- **Up to 20% higher success rate** over JSON and text action formats on complex tool-use benchmarks
- **CodeActInstruct**: 7K multi-turn agent interaction trajectories for instruction tuning
- **CodeActAgent**: Fine-tuned Llama-2 and Mistral models that can execute code, use libraries, and self-debug
- Demonstrated that code is a superior action representation because it supports:
  - **Composition**: Chain multiple tool calls in a single action
  - **Control flow**: Loops, conditionals, error handling
  - **Self-debugging**: Inspect error tracebacks and revise code
  - **Existing libraries**: Use any Python package without pre-defining tool schemas

## Method
### CodeAct Framework
- **Three roles**: Agent (LLM), User (human), Environment (Python interpreter + tools)
- Agent generates Python code blocks as actions
- Python interpreter executes code, returns stdout/stderr as observations
- Agent can dynamically revise code based on execution results
- Multi-turn interaction: agent ↔ environment ↔ user

### Why Code > JSON/Text
1. **Larger action space**: Any Python expression vs. pre-defined tool calls
2. **Tool composition**: Multiple tool calls in one code block (e.g., `result = tool_a(tool_b(x))`)
3. **Control flow**: Loops over results, conditional branching, error handling
4. **Self-debugging**: Read tracebacks, fix bugs, retry
5. **Library access**: Use pandas, numpy, sklearn, etc. without explicit tool definitions

### CodeActInstruct Dataset
- 7K multi-turn interaction trajectories across 5 domains:
  - Web search (HotpotQA)
  - Math reasoning (GSM8K, MATH)
  - Tabular reasoning (WikiTableQuestions)
  - Text-to-SQL (BIRD)
  - General Python tasks
- Generated using GPT-4 with CodeAct framework
- Filtered by successful task completion

### CodeActAgent Training
- Full-parameter SFT from Llama-2-7B and Mistral-7B
- Mixed training: CodeActInstruct + general conversation data (ShareGPT, OpenOrca)
- Sequence length 4,096, ChatML format

## Results
- **API-Bank**: CodeAct outperforms JSON/text across all 17 tested LLMs
- **M³ToolEval** (new benchmark with complex multi-tool tasks):
  - CodeAct achieves 20%+ higher success rates than alternatives
  - Benefits increase with task complexity (more tools, more steps)
- **CodeActAgent (Mistral)**: 10%+ improvement over base model on agent tasks, matches GPT-3.5 level performance
- **Fewer interactions needed**: Code actions accomplish more per step via composition, reducing total interaction turns

## Connections
- **Builds on**: [[sources/react]] (Thought-Action-Observation loop), tool-use LLMs
- **Directly inspired**: Hugging Face smolagents (uses CodeAct as default action paradigm)
- **Key concepts**: [[concepts/agents]], [[concepts/tool-use]]
- **Related**: [[sources/llamafactory]] (fine-tuning framework), [[sources/llama-3|Llama 3]] (tool-use training)
- **GitHub**: [xingyaoww/code-act](https://github.com/xingyaoww/code-act) — 1.6K ⭐

## Citation
> Wang et al., "Executable Code Actions Elicit Better LLM Agents," ICML 2024, arXiv:2402.01030, 2024.
> https://huggingface.co/papers/2402.01030
