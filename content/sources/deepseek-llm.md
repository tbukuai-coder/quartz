---
type: source
arxiv_id: "2401.02954"
title: "DeepSeek LLM: Scaling Open-Source Language Models with Longtermism"
authors: ["DeepSeek-AI", "Xiao Bi", "Deli Chen"]
date: 2024-01-05
org: "DeepSeek"
tags: [pre-training, scaling-laws, open-model, alignment, 2024]
upvotes: 55
---

# DeepSeek LLM

> DeepSeek's foundational LLM project that revisited scaling laws and introduced 7B and 67B open models surpassing LLaMA-2-70B and GPT-3.5.

## Key Contributions
- Revisited **scaling laws** with new findings: optimal model/data ratio differs from Chinchilla; derived new scaling curves for 7B and 67B configurations
- Trained **DeepSeek LLM 7B and 67B** on 2T tokens of primarily Chinese and English data
- **DeepSeek-67B-Chat** surpasses LLaMA-2-70B-Chat on most benchmarks and matches GPT-3.5 on open-ended evaluations
- Demonstrated effective **two-stage SFT + DPO** alignment pipeline for chat models
- Released fully open weights under a permissive license, becoming the foundation for later DeepSeek-V2, V3, and R1

## Method
**Pre-training**: Decoder-only Transformer with 2T tokens. Architecture innovations include **Multi-Head Latent Attention (MLA)** precursors in the design. Data pipeline covers web, books, code, math, and academic sources with careful quality filtering and deduplication. New scaling law analysis found that compute-optimal configurations may favor larger models than Chinchilla predicts when data quality is high.

**Alignment**: Two-stage pipeline — (1) Supervised Fine-Tuning on curated instruction data (1.5M examples), (2) Direct Preference Optimization (DPO) on human preference data. Chat models include system prompts for helpfulness and safety.

## Results
- **DeepSeek-67B** outperforms LLaMA-2-70B on MMLU (71.3 vs 69.8), GSM8K (63.4 vs 54.4), HumanEval (73.2 vs 29.9)
- **DeepSeek-67B-Chat** competitive with GPT-3.5-turbo on MT-Bench and AlpacaEval
- **DeepSeek-7B** outperforms LLaMA-2-7B on most benchmarks despite similar scale
- Scaling law predictions validated: model performance follows predicted curves up to 67B

## Datasets Used
- Custom 2T token corpus (web, books, code, math, academic)
- Alpaca-format and ShareGPT-format instruction data for SFT
- Human preference data for DPO

## Models Released
- [[entities/models/deepseek|DeepSeek LLM]] 7B Base/Chat, 67B Base/Chat (open weights)

## Connections
- **Builds on**: [[sources/chinchilla|Chinchilla]] (scaling laws), [[sources/llama|LLaMA]] (architecture template), [[sources/dpo|DPO]] (alignment)
- **Foundation for**: [[sources/deepseek-v3|DeepSeek-V3]], [[sources/deepseekmath|DeepSeekMath]], [[sources/deepseek-r1|DeepSeek-R1]]
- **Related orgs**: [[entities/orgs/deepseek|DeepSeek]]
- **Related concepts**: [[concepts/scaling-laws|Scaling Laws]], [[concepts/pre-training|Pre-training]], [[concepts/dpo|DPO]]

## Citation
> DeepSeek-AI, "DeepSeek LLM: Scaling Open-Source Language Models with Longtermism," arXiv:2401.02954, 2024.
