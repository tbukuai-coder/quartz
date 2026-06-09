---
type: source
arxiv_id: "2307.09702"
title: "Efficient Guided Generation for Large Language Models"
authors: ["Brandon T. Willard", "Rémi Louf"]
date: 2023-07-19
org: "Normal Computing"
tags: [structured-generation, inference, agents, tool-use, 2023]
upvotes: 8
---

# Efficient Guided Generation for Large Language Models (Outlines)

> A framework that reformulates constrained text generation as finite-state machine transitions, enabling efficient generation of text conforming to regular expressions and context-free grammars with minimal overhead.

## Key Contributions
- Reformulated neural text generation as transitions between states of a finite-state machine (FSM), enabling exact enforcement of structural constraints
- Introduced vocabulary indexing: a pre-computed mapping from FSM states to valid token sets, making guided generation O(1) per token (vs. O(N×L) for naive approaches)
- Extended the FSM approach to context-free grammars via pushdown automata, supporting complex structures like JSON, Python, SQL
- Implemented in the open-source Outlines library (13K+ GitHub stars), the de facto standard for structured LLM generation
- Model-agnostic: works with any autoregressive LLM without fine-tuning

## Method
The core insight is that regular expression matching during generation can be decomposed into FSM transitions:

1. **FSM Construction**: Convert the target regular expression (or grammar) into a finite-state machine
2. **Vocabulary Indexing** (one-time, cached):
   - For each FSM state, determine which vocabulary tokens are valid (would lead to a valid next state)
   - Build an index: `state → set of allowed token IDs`
   - This is computed once per (regex, vocabulary) pair and cached
3. **Generation**: At each decoding step:
   - Look up current FSM state → get allowed tokens
   - Apply boolean mask to logits (set disallowed tokens to -∞)
   - Sample from masked distribution
   - Update FSM state based on generated token

**Extension to CFGs**: For context-free grammars (e.g., JSON Schema), the approach uses pushdown automata with a stack for tracking nested structures. The indexing approach still applies, though the state space is larger.

**Key advantage over prior work (e.g., Guidance)**: Previous methods used partial regex matching applied from the start of the sequence at each step, resulting in O(N×L) complexity. Outlines' FSM indexing reduces this to O(1) per generation step after the initial index construction.

## Results
- **Speed**: Outlines generates structured text with negligible overhead vs. unconstrained generation (after initial index build)
- **Correctness**: 100% of outputs conform to the specified pattern — guaranteed by construction
- **Comparison with Guidance**: Outlines is orders of magnitude faster for complex patterns, as Guidance's complexity grows linearly with sequence length

## Applications
- **JSON mode**: Guarantee valid JSON output matching a schema (critical for tool use and agents)
- **Function calling**: Ensure LLM outputs valid function signatures and arguments
- **Data extraction**: Extract structured information from text with guaranteed format
- **Code generation**: Enforce syntactic correctness of generated code
- **Classification**: Constrain output to a fixed set of labels

## Connections
- Related concepts: [[concepts/structured-generation|Structured Generation]], [[concepts/agents|LLM Agents & Tool Use]], [[concepts/llm-serving|LLM Serving & Inference]]
- Integrated into: [[sources/vllm|vLLM]] (via outlines backend), [[sources/sglang|SGLang]], HF TGI
- Related: Guidance (Microsoft), LMQL, jsonformer
- Enables: Reliable [[sources/react|ReAct]]-style agent loops, [[sources/codeact|CodeAct]] structured outputs
- Ecosystem: 13K+ GitHub stars, de facto standard for structured generation in production LLM deployments

## Citation
> Willard and Louf, "Efficient Guided Generation for Large Language Models," arXiv:2307.09702, 2023.
