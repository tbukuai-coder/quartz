---
type: source
arxiv_id: "2302.01318"
title: "Toolformer: Language Models Can Teach Themselves to Use Tools"
authors: ["Timo Schick", "Jane Dwivedi-Yu", "Roberto Dessì", "et al."]
date: 2023-02-09
org: "Meta AI"
tags: [agents, tool-use, foundational, 2023]
upvotes: 10
---

# Toolformer: Language Models Can Teach Themselves to Use Tools

> Showed that LLMs can **learn to use tools** (calculator, search, translator, calendar, QA) by **self-supervised API call insertion** into training text — without human demonstrations. The model decides *when and how* to call tools, filling a key gap between pure language modeling and agentic behavior.

## Key Contributions
- **Self-supervised tool learning**: LLM generates API calls, filters by usefulness (reduces perplexity), and trains on the augmented data
- **Multiple tools**: Calculator, Q&A system, Wikipedia search, machine translator, calendar
- **No human annotation**: The model teaches itself which tools to use and when
- **Outperforms larger models**: 6.7B Toolformer outperforms 175B GPT-3 on tasks requiring tools (math, factual QA)
- **Inline API calls**: Tools are called within the text generation process as special tokens

## Method
```
Input text: "The Eiffel Tower is [QA("height of Eiffel Tower") → 330m] 330 meters tall"
```

1. **Sample API calls**: For each position in training text, sample potential tool calls
2. **Execute calls**: Run tools and get responses
3. **Filter by usefulness**: Keep calls that reduce next-token perplexity
4. **Fine-tune**: Train model on text augmented with useful API calls
5. **Inference**: Model generates API call tokens when beneficial, executes them, continues

## Results
| Task | GPT-3 (175B) | Toolformer (6.7B) | Tool Used |
|---|---|---|---|
| Math (ASDiv) | 52.2% | **63.5%** | Calculator |
| QA (Web Questions) | 17.2% | **25.5%** | QA system |
| Temporal | 30.0% | **46.0%** | Calendar |
| Translation | 11.5 BLEU | **18.0 BLEU** | MT system |

6.7B model with tools beats 175B model without tools on tool-appropriate tasks.

## Impact
- **Foundational agent paper**: Established the paradigm of LLMs using tools, predating function calling APIs
- Influenced: [[sources/react|ReAct]] (reasoning + acting), [[sources/codeact|CodeAct]], ChatGPT plugins
- Concept of "tool use as self-supervised learning" influenced all subsequent agent architectures
- Showed that **small models + tools > large models** for specific tasks

## Connections
- Related: [[sources/react|ReAct]], [[sources/codeact|CodeAct]], [[sources/swe-agent|SWE-agent]]
- Org: [[entities/orgs/meta|Meta AI]]
- Concepts: [[concepts/agents|LLM Agents & Tool Use]]

## Citation
> Schick et al., "Toolformer: Language Models Can Teach Themselves to Use Tools," NeurIPS 2023, arXiv:2302.01318.
