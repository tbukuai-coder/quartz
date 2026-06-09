---
type: source
arxiv_id: "2005.14165"
title: "Language Models are Few-Shot Learners"
authors: ["Tom Brown", "Benjamin Mann", "Nick Ryder", "et al."]
date: 2020-05-28
org: "OpenAI"
tags: [foundational, pre-training, few-shot, scaling]
upvotes: 0
---

# GPT-3: Language Models are Few-Shot Learners

> The paper that **launched the modern LLM era** — demonstrated that a 175B parameter model can perform tasks via **in-context learning** (few-shot prompting) without fine-tuning. GPT-3 showed that scale alone unlocks emergent capabilities, catalyzing the entire open-source LLM movement as researchers raced to replicate and surpass it.

## Key Contributions
- **In-context learning**: Models can learn tasks from a few examples in the prompt, without gradient updates
- **Scaling unlocks capabilities**: 175B parameters showed emergent abilities (arithmetic, translation, coding) not present at smaller scales
- **Few-shot prompting paradigm**: Established the pattern of task specification via natural language instructions + examples
- **175B parameters**: Largest model at the time, trained on 300B tokens
- **Foundational benchmarks**: Established evaluation patterns used by all subsequent LLMs

## Architecture & Training
- **175B parameters**: 96 layers, 12288 hidden dim, 96 attention heads
- **Training data**: ~300B tokens from Common Crawl (filtered), WebText2, Books1/2, Wikipedia
- **Training compute**: ~3640 petaflop/s-days
- **Context window**: 2048 tokens

## Impact — The Catalyst for Open Source
GPT-3's closed nature directly motivated the open-source LLM movement:
- **[[entities/orgs/eleutherai|EleutherAI]]** formed in 2020 specifically to replicate GPT-3 openly → [[sources/gpt-neox|GPT-NeoX-20B]]
- **[[sources/bloom|BLOOM]]** (BigScience): Open 176B to match GPT-3 scale
- **[[sources/llama|LLaMA]]** (Meta): Showed GPT-3 quality at 7–65B parameters
- **[[sources/instructgpt|InstructGPT]]**: GPT-3 + RLHF → foundation of ChatGPT
- **[[sources/chinchilla|Chinchilla]]**: Showed GPT-3 was undertrained (should use more tokens, fewer params)

## Connections
- Extended by: [[sources/instructgpt|InstructGPT]], [[sources/gpt-4|GPT-4]]
- Replicated by: [[sources/gpt-neox|GPT-NeoX]], [[sources/bloom|BLOOM]]
- Surpassed by: [[sources/llama|LLaMA]] (much smaller, similar quality)
- Org: [[entities/orgs/openai|OpenAI]]
- Concepts: [[concepts/scaling-laws]], [[concepts/pre-training]], [[concepts/instruction-tuning]]

## Citation
> Brown et al., "Language Models are Few-Shot Learners," NeurIPS 2020, arXiv:2005.14165.
