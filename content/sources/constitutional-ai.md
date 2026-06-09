---
type: source
arxiv_id: "2212.08073"
title: "Constitutional AI: Harmlessness from AI Feedback"
authors: ["Yuntao Bai", "Saurav Kadavath", "Sandipan Kundu", "et al."]
date: 2022-12-15
org: "Anthropic"
tags: [alignment, safety, rlaif, foundational]
upvotes: 4
---

# Constitutional AI: Harmlessness from AI Feedback

> Introduced **RLAIF (RL from AI Feedback)** — training a harmless AI assistant using a set of principles ("constitution") and self-critique, without human labels for harmful outputs.

## Key Contributions
- Introduced the **Constitutional AI (CAI)** framework — align models using a written set of principles
- Demonstrated **RLAIF**: the AI generates its own preference labels based on the constitution, replacing human annotators for safety training
- Showed **self-critique + revision** as a scalable safety technique: the model critiques its own outputs and revises them
- Reduced the need for human annotation of harmful content (better for labeler wellbeing)
- The "constitution" is a small set of human-readable principles — transparent and auditable

## Method
### Supervised Phase (Critiqued Revision)
1. Generate responses to potentially harmful prompts (using a helpful-only model)
2. Ask the model to **critique** its own response based on constitutional principles
3. Ask the model to **revise** the response to comply with the principles
4. Fine-tune on the revised outputs (SL-CAI)

### RL Phase (RLAIF)
1. Generate pairs of responses to the same prompt
2. Ask the model which response is better **according to the constitution** (AI feedback)
3. Train a **preference model** on the AI-generated comparisons
4. Optimize with RL (PPO) against this preference model

The constitution is a set of ~15 principles like "Choose the response that is less harmful," "Choose the response that is most honest," etc.

## Connections
- **Builds on**: [[sources/instructgpt]] (RLHF framework)
- **Influenced**: [[sources/zephyr]] (AI feedback for alignment), the entire RLAIF movement
- **Key concepts**: [[concepts/constitutional-ai]], [[concepts/rlhf]]
- **Organizations**: [[entities/orgs/anthropic]]

## Citation
> Bai et al., "Constitutional AI: Harmlessness from AI Feedback," arXiv:2212.08073, 2022.
> https://huggingface.co/papers/2212.08073
