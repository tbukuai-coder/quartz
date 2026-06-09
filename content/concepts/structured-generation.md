---
type: concept
tags: [inference, structured-generation, agents, tool-use, serving]
---

# Structured Generation

> Constraining LLM output to conform to a **predefined format** (JSON schema, regex, grammar) — guaranteeing syntactically valid outputs for tool use, data extraction, and agent workflows.

## Overview
LLMs generate text token by token with no inherent guarantee that the output will be valid JSON, match a schema, or follow a grammar. Structured generation solves this by masking invalid tokens during decoding — ensuring 100% format compliance by construction, not by prompting. This is critical for production systems where a single malformed JSON response can crash a pipeline.

## Why It Matters
- **Tool use / function calling**: Agents must produce valid function signatures and arguments — one invalid JSON character breaks the tool call
- **Data extraction**: Extracting structured records from text requires guaranteed schema compliance
- **Classification**: Constraining output to a fixed label set eliminates hallucinated categories
- **Code generation**: Enforcing syntactic correctness reduces errors
- **API backends**: JSON mode is now a standard feature of LLM APIs (OpenAI, Anthropic, open-source)

## How It Works

### FSM-Based Approach (Outlines)
[[sources/outlines|Outlines]] reformulated structured generation as finite-state machine (FSM) transitions:

1. **Compile**: Convert regex/grammar → finite-state machine (or pushdown automaton for CFGs)
2. **Index** (one-time, cached): For each FSM state, precompute which vocabulary tokens lead to a valid next state
3. **Generate**: At each decoding step:
   - Look up current state → get set of valid token IDs
   - Mask invalid tokens (set logits to -∞)
   - Sample from masked distribution
   - Advance FSM state

This achieves **O(1) per-token overhead** after initial compilation (vs. O(N×L) for naive regex matching).

### Grammar-Based Approach
For context-free grammars (JSON Schema, SQL, Python):
- Uses pushdown automata (FSM + stack) to handle nested structures
- [[sources/sglang|SGLang]]'s compressed FSM can skip multiple constrained tokens at once, reducing overhead further
- xgrammar library provides efficient grammar-constrained decoding

### Speculative Grammar Decoding
Combine [[concepts/speculative-decoding|speculative decoding]] with grammar constraints:
- Draft model proposes tokens; grammar mask applied during verification
- Achieves structured generation with speculative speedups

## Key Methods

| System | Approach | Integration | Key Feature |
|---|---|---|---|
| [[sources/outlines\|Outlines]] | FSM + vocabulary indexing | vLLM, TGI, standalone | De facto standard, 13K+ ⭐ |
| [[sources/sglang\|SGLang]] | Compressed FSM | Built-in | Multi-token jumps, up to 6.4× throughput |
| Guidance (Microsoft) | Token healing + CFG | Standalone | Early pioneer |
| xgrammar | Grammar-based | MLC-LLM, SGLang | High-performance grammar engine |
| lm-format-enforcer | Schema → regex → FSM | vLLM, TGI | JSON Schema specialization |

## JSON Mode
The most common structured generation use case:

```
Input: "Extract name, age, and city from: 'John is 30 and lives in NYC'"
Schema: {"name": str, "age": int, "city": str}
Output: {"name": "John", "age": 30, "city": "NYC"}  ← guaranteed valid
```

Every major serving framework now supports JSON mode:
- [[sources/vllm|vLLM]]: Via Outlines backend (default) or xgrammar
- [[sources/sglang|SGLang]]: Native compressed FSM
- TGI: Via Outlines integration
- OpenAI API: `response_format={"type": "json_schema", ...}`

## Impact on Agents
Structured generation is foundational for reliable [[concepts/agents|LLM agents]]:
- [[sources/react|ReAct]]-style agents need valid action format at every step
- [[sources/codeact|CodeAct]] agents need syntactically valid Python code
- Tool-calling requires valid function call JSON
- [[sources/qwen3|Qwen3]] and Llama 3 include structured output training in post-training

## Key Papers
- [[sources/outlines]] — FSM-based structured generation (2023)
- [[sources/sglang]] — Compressed FSM for structured output (2023)

## See Also
- [[concepts/llm-serving]] — Structured generation is a serving-layer feature
- [[concepts/agents]] — Primary consumer of structured outputs
- [[concepts/speculative-decoding]] — Can be combined with grammar constraints