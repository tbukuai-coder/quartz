---
type: source
arxiv_id: "2203.02155"
title: "Training language models to follow instructions with human feedback"
authors: ["Long Ouyang", "Jeff Wu", "Xu Jiang", "et al."]
date: 2022-03-04
org: "OpenAI"
tags: [alignment, rlhf, foundational]
upvotes: 24
---

# InstructGPT: Training Language Models to Follow Instructions with Human Feedback

> Established the **RLHF pipeline** (SFT → Reward Model → PPO) for aligning language models with human intent, producing InstructGPT which was preferred over the 100× larger GPT-3.

## Key Contributions
- Defined the canonical **three-stage RLHF pipeline**: (1) Supervised fine-tuning on demonstrations, (2) Reward model training on human comparisons, (3) PPO optimization against the reward model
- Showed that a **1.3B parameter InstructGPT** is preferred by humans over the **175B GPT-3**
- Demonstrated that alignment is largely orthogonal to scale — small aligned models beat large unaligned ones
- Established that RLHF reduces **toxicity** and improves **truthfulness** with minimal performance regression on benchmarks

## Method
1. **SFT Stage**: Fine-tune GPT-3 on ~13K demonstration prompts written by human labelers
2. **Reward Model**: Train a 6B model on ~33K human comparison pairs (labelers rank model outputs)
3. **PPO**: Optimize the SFT model against the reward model using Proximal Policy Optimization, with a KL penalty to prevent divergence from the SFT model

The key insight: human preferences are easier to provide than demonstrations, and RL can leverage them effectively.

## Results
- InstructGPT 1.3B preferred over GPT-3 175B by human evaluators
- Reduced toxic outputs by ~25% compared to GPT-3
- Improved truthfulness on TruthfulQA
- Small regression on some academic benchmarks (alignment tax)

## Connections
- **Builds on**: [[sources/attention-is-all-you-need]] (Transformer architecture)
- **Influenced**: [[sources/dpo]], [[sources/constitutional-ai]], [[sources/zephyr]], [[sources/llama-2]], [[sources/deepseek-r1]]
- **Key concepts**: [[concepts/rlhf]], [[concepts/fine-tuning]], [[concepts/instruction-tuning]]
- **Organizations**: [[entities/orgs/openai]]

## Citation
> Ouyang et al., "Training language models to follow instructions with human feedback," arXiv:2203.02155, 2022.
> https://huggingface.co/papers/2203.02155
