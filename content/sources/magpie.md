---
type: source
arxiv_id: "2406.08464"
title: "Magpie: Alignment Data Synthesis from Scratch by Prompting Aligned LLMs with Nothing"
authors: ["Zhangchen Xu", "Fengqing Jiang", "Luyao Niu", "Yuntian Deng", "Radha Poovendran", "Yejin Choi", "Bill Yuchen Lin"]
date: 2024-06-12
org: "University of Washington"
tags: [alignment, synthetic-data, sft, dpo, 2024]
upvotes: 72
---

# Magpie: Alignment Data Synthesis from Scratch by Prompting Aligned LLMs with Nothing

> Discovers that aligned LLMs like Llama-3-Instruct will **auto-generate user queries** when prompted with only the pre-query template (no user message), enabling the synthesis of millions of high-quality instruction-response pairs with zero human input.

## Key Contributions
- **Key insight**: Aligned LLMs with chat templates can generate user instructions when given only the system prompt and pre-query markers — the model "hallucinates" a plausible user query, then answers it
- **Magpie pipeline**: Scalable method to synthesize arbitrarily large alignment datasets from any instruction-tuned model
- Generated **4 million** instruction-response pairs from Llama-3-Instruct (8B and 70B)
- Models SFT'd on Magpie data **match or exceed** official Llama-3-8B-Instruct on alignment benchmarks, despite Meta using 10M+ datapoints with SFT + DPO
- Extensions for filtering, multi-turn, DPO preference pairs, domain-specific, and multilingual data generation
- Released datasets, code, and MagpieLM models

## Method
### Core Pipeline
1. **Query generation**: Feed the model only the pre-query template `<|begin_of_text|><|start_header_id|>user<|end_header_id|>\n\n` — the model auto-regressively generates a user instruction
2. **Response generation**: Append the generated query and post-query template, let the model generate a response
3. **Filtering** (optional): Score by quality, difficulty, input length, reward model score, etc.

### Extensions
- **Magpie-MT**: Multi-turn conversations by repeating the query-response cycle
- **Magpie-DPO**: Generate multiple responses per query, use reward model to select chosen/rejected pairs for [[concepts/dpo|DPO]]
- **Domain control**: Prepend system prompts to steer instruction topics
- **Cross-model**: Use one model to generate queries, another to generate responses

### Key Design Decisions
- Temperature and top-p affect quality/difficulty/diversity trade-off
- Higher temperature → more diverse but lower quality instructions
- 70B model (Magpie-Pro) generates higher quality than 8B (Magpie-Air)
- Quality/difficulty filtering provides additional 2–5% improvement

## Results
- **Magpie-Air-DPO** (300K SFT + DPO from Llama-3-8B-Instruct): 64.2 on AlpacaEval 2.0 LC, vs 22.9 for official Llama-3-8B-Instruct
- **Magpie-Pro-SFT** (300K from 70B): surpasses all prior open SFT datasets (ShareGPT, WildChat, Evol-Instruct, UltraChat, OpenHermes)
- SFT-only Magpie models outperform baselines that used both SFT + DPO (e.g., [[sources/zephyr|Zephyr]]-style dDPO with [[entities/datasets/ultrafeedback|UltraFeedback]])
- Cost: 4M instances generated in ~5.5 hours on 4× A100 GPUs (~$200)
- Safety: <1% potentially harmful content (per Llama-Guard-2)
- Works across model families: Llama-3, Qwen2, Phi-3, Gemma-2

## Connections
- **Builds on**: [[sources/self-instruct]] (synthetic instruction generation, but Magpie needs no seed tasks), chat template design of [[sources/llama-3|Llama 3]]
- **Related**: [[sources/zephyr]] (AI-generated alignment data), [[concepts/instruction-tuning]], [[concepts/dpo]]
- **Used by**: SmolTalk dataset for [[sources/smollm2|SmolLM2]]
- **Datasets**: [[entities/datasets/ultrachat]], [[entities/datasets/ultrafeedback]] (baselines Magpie outperforms)
- **Key concepts**: [[concepts/synthetic-data]], [[concepts/instruction-tuning]]

## Citation
> Xu et al., "Magpie: Alignment Data Synthesis from Scratch by Prompting Aligned LLMs with Nothing," arXiv:2406.08464, 2024.
> https://huggingface.co/papers/2406.08464
