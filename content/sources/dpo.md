---
type: source
arxiv_id: "2305.18290"
title: "Direct Preference Optimization: Your Language Model is Secretly a Reward Model"
authors: ["Rafael Rafailov", "Archit Sharma", "Eric Mitchell", "Stefano Ermon", "Christopher D. Manning", "Chelsea Finn"]
date: 2023-05-29
org: "Stanford University"
tags: [alignment, dpo, foundational]
upvotes: 64
---

# Direct Preference Optimization (DPO)

> Showed that the RLHF objective can be **reparameterized** to directly optimize a language model on preference data, eliminating the need for a separate reward model and PPO training — making alignment dramatically simpler and more stable.

## Key Contributions
- Proved that the optimal policy under the RLHF objective has a **closed-form solution** expressible as a function of the reward
- Derived a **simple classification loss** (DPO loss) that directly optimizes the policy on preference pairs
- Eliminated the need for: reward model fitting, PPO sampling, reward normalization
- Showed DPO matches or exceeds PPO-based RLHF on sentiment control, summarization, and dialogue
- Became the **dominant alignment method** in the open-source ecosystem

## Method
The key insight: under the Bradley-Terry preference model, the optimal policy satisfies:

```
r(x, y) = β log[π*(y|x) / π_ref(y|x)] + β log Z(x)
```

This means the reward is implicitly defined by the policy itself. Substituting this into the preference objective gives the **DPO loss**:

```
L_DPO = -E[log σ(β log(π_θ(y_w|x)/π_ref(y_w|x)) - β log(π_θ(y_l|x)/π_ref(y_l|x)))]
```

Where `y_w` is the preferred and `y_l` is the dispreferred response. This is just a binary cross-entropy loss on the log-ratio margin between the policy and reference model. No reward model, no RL loop — just standard supervised training.

## Results
- **Sentiment control**: Matched RLHF (PPO) performance
- **Summarization**: Matched or exceeded RLHF on human evaluations
- **Dialogue (Anthropic HH)**: Comparable to RLHF with much simpler training
- Dramatically reduced training complexity, memory, and compute requirements

## Connections
- **Builds on**: [[sources/instructgpt]] (RLHF framework it simplifies)
- **Influenced**: [[sources/zephyr]] (dDPO), [[sources/deepseekmath]] (GRPO extends DPO ideas)
- **Key concepts**: [[concepts/dpo]], [[concepts/rlhf]], [[concepts/fine-tuning]]
- **Variants**: ORPO, SimPO, KTO, IPO, CPO — see [[concepts/dpo]]
- **Organizations**: Stanford

## Citation
> Rafailov et al., "Direct Preference Optimization: Your Language Model is Secretly a Reward Model," arXiv:2305.18290, 2023.
> https://huggingface.co/papers/2305.18290
