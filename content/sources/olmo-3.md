---
type: source
arxiv_id: "2512.13961"
title: "OLMo 3"
authors: ["Team OLMo", "Allyson Ettinger", "Amanda Bertsch", "et al."]
date: 2025-12-18
org: "AllenAI"
tags: [open-science, reasoning, function-calling, fully-open, 2025]
upvotes: 32
---

# OLMo 3

> A family of fully-open language models at 7B and 32B scales — the strongest fully-open thinking model released to date, with every stage, checkpoint, data point, and dependency publicly available.

## Key Contributions
- **OLMo 3 Think 32B** is the **strongest fully-open thinking model** released to date, targeting long-context reasoning, function calling, coding, instruction following, general chat, and knowledge recall
- Continues AllenAI's commitment to **radical openness**: releases the entire model flow — every training stage, checkpoint, data point, and dependency
- Introduces **thinking mode** (Think variant) alongside standard instruction-following variants
- Available at both **7B and 32B** parameter scales, covering the most practical deployment sizes

## Method
OLMo 3 follows AllenAI's fully-open paradigm established with [[sources/olmo|OLMo]] and [[sources/olmo-2|OLMo 2]]:

**Model construction targets**:
- Long-context reasoning
- Function calling
- Coding
- Instruction following
- General chat
- Knowledge recall

**Full lifecycle release**: Unlike most "open-weight" models that only release final checkpoints, OLMo 3 provides:
- All pre-training data (following the [[entities/datasets/dolma|Dolma]] tradition)
- Training code and configurations
- All intermediate checkpoints
- Evaluation harnesses and results
- Every dependency used in the build process

**Think variant**: OLMo 3 Think 32B incorporates extended reasoning capabilities, following the broader trend of thinking/non-thinking mode models (cf. [[sources/qwen3|Qwen3]], [[sources/llama-nemotron|Llama-Nemotron]]).

## Results
- **OLMo 3 Think 32B**: Strongest fully-open thinking model at release
- Excels across targeted capabilities: long-context reasoning, function calling, coding, instruction following, general chat, and knowledge recall
- Represents a significant leap from [[sources/olmo-2|OLMo 2]], which itself improved substantially over [[sources/olmo|OLMo]]

## Models Released
- **OLMo 3 7B** — fully-open 7B model
- **OLMo 3 32B** — fully-open 32B model
- **OLMo 3 Think 32B** — thinking variant, flagship model
- All training data, code, checkpoints, and dependencies

## Datasets Used
- Training data fully released (following Dolma/OLMo tradition)
- [[entities/datasets/dolma|Dolma]] ecosystem

## Connections
- Builds on: [[sources/olmo|OLMo]], [[sources/olmo-2|OLMo 2]]
- Competes with: [[sources/llama-3|Llama 3]], [[sources/qwen25|Qwen2.5]], [[sources/gemma-2|Gemma 2]] (at similar scales)
- Distinguished from: [[sources/llama-3|Llama]] (open-weight only) — OLMo 3 is fully-open
- Related concepts: [[concepts/pre-training]], [[concepts/fine-tuning]], [[concepts/chain-of-thought]]
- From: [[entities/orgs/allenai|AllenAI]]

## Citation
> Team OLMo, "OLMo 3," arXiv:2512.13961, 2025.
