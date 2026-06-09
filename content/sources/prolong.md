---
type: source
arxiv_id: "2410.02660"
title: "How to Train Long-Context Language Models (Effectively)"
authors: ["Tianyu Gao", "Alexander Wettig", "Howard Yen", "Danqi Chen"]
date: 2024-10-03
org: "Princeton University"
tags: [long-context, training, sft, 2024]
upvotes: 2
---

# ProLong (How to Train Long-Context LMs)

> A comprehensive study on extending LLM context via continued pretraining + long-context SFT, producing ProLong-8B models that outperform Llama-3.1-8B on long-context tasks.

## Key Contributions
- Provided a **systematic recipe** for training long-context LLMs via continued training
- Showed that **long-context SFT data is critical** — models need diverse long-context instruction data, not just long pretraining
- Produced **ProLong-8B-64k** and **ProLong-8B-512k** that outperform Llama-3.1-8B-Instruct on RULER and other long-context benchmarks
- Analyzed **perplexity vs real-world performance**: low perplexity on long sequences ≠ good long-context task performance (needle-in-haystack, reasoning)
- Released training data, code, and models

## Method
Two-stage recipe:
1. **Continued pretraining**: Train on mix of short and long documents with progressively increasing context length
2. **Long-context SFT**: Fine-tune on diverse instruction data including long-document QA, summarization, multi-hop reasoning at target context length

Key finding: models need to see diverse **tasks** at long context lengths during SFT, not just long text during pretraining. Simply extending pretraining isn't enough.

## Results
- **RULER**: ProLong-8B-64k surpasses Llama-3.1-8B-Instruct at matched context lengths
- **Needle-in-Haystack**: Near-perfect retrieval at 64K tokens
- **Long-document QA**: Consistent improvement over base Llama-3 on quality and recall
- **Short-context preservation**: Original short-context performance maintained

## Connections
- **Builds on**: [[sources/llama-3|Llama 3]], [[sources/longrope|LongRoPE]], [[sources/yarn|YaRN]]
- **Related concepts**: [[concepts/long-context|Long Context]], [[concepts/instruction-tuning|Instruction Tuning]], [[concepts/fine-tuning|Fine-tuning]]
- **Complements**: LongRoPE (positional extension) — ProLong shows that data/SFT matters more than just positional tricks

## Citation
> Gao et al., "How to Train Long-Context Language Models (Effectively)," arXiv:2410.02660, 2024.
