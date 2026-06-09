---
type: source
arxiv_id: "2402.13753"
title: "LongRoPE: Extending LLM Context Window Beyond 2 Million Tokens"
authors: ["Yiran Ding", "Li Lyna Zhang", "Chengruidong Zhang", "Yuanyuan Xu", "Ning Shang", "Jiahang Xu", "Fan Yang", "Mao Yang"]
date: 2024-02-21
org: "Microsoft"
tags: [long-context, positional-encodings, rope, efficiency, 2024]
upvotes: 116
---

# LongRoPE

> Extends pre-trained LLM context windows to 2,048K tokens with only 1K fine-tuning steps at 256K training length, while maintaining short-context performance.

## Key Contributions
- First method to extend LLM context windows to **2 million tokens** (2048K), far beyond the previous ~128K limit
- Identified and exploited **two forms of non-uniformity** in RoPE positional interpolation: across dimensions and across token positions
- Achieved **8× context extension without any fine-tuning** through efficient evolutionary search for optimal RoPE rescale factors
- Introduced a **progressive extension strategy**: fine-tune to 256K → second interpolation to 2048K
- Showed that **readjusting on 8K length** recovers short-context performance — no accuracy loss at original context

## Method
LongRoPE addresses three key challenges: (1) different RoPE dimensions have different sensitivity to interpolation, (2) token positions in longer sequences need non-uniform rescaling, and (3) naive extension to very long contexts degrades short-context performance.

The method uses an **evolutionary search** to find optimal rescale factors for each RoPE dimension separately, minimizing perplexity on validation data. A **progressive strategy** first fine-tunes to 256K (1K steps), then applies a second non-uniform interpolation to reach 2048K. Finally, rescale factors are readjusted on 8K sequences to preserve original-length performance.

## Results
- **LLaMA2-7B**: Extended to 2048K with passkey retrieval accuracy maintained; perplexity 7.08 at 2048K on Books3
- **Mistral-7B**: Extended to 256K, outperforming YaRN and other baselines on Proof-pile and PG19
- **Short-context preservation**: Maintains >95% accuracy on original 4K benchmarks (ARC, HellaSwag, MMLU, TruthfulQA, Winogrande)
- **Efficiency**: Only 1,000 fine-tuning steps at 256K length on 16 A100 GPUs

## Datasets Used
- PG19, Proof-pile, Books3, RULER (long-context eval)

## Models Released
- Extended LLaMA2-7B (128K, 256K, 2048K variants)
- Extended Mistral-7B (128K, 256K variants)

## Connections
- **Builds on**: [[sources/rope|RoPE]], [[sources/yarn|YaRN]], [[concepts/positional-encodings|Positional Encodings]]
- **Related**: [[concepts/long-context|Long Context]], [[concepts/flash-attention|FlashAttention]] (required for training/inference)
- **Influenced**: LongRoPE2 (2025), Microsoft Phi long-context variants
- **Compared with**: YaRN, PI (Positional Interpolation), NTK-aware scaling
- **Related concepts**: [[concepts/kv-cache|KV Cache]] (memory grows linearly with context)

## Citation
> Ding et al., "LongRoPE: Extending LLM Context Window Beyond 2 Million Tokens," arXiv:2402.13753, 2024.
