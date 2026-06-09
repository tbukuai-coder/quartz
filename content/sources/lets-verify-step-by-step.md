---
type: source
arxiv_id: "2305.20050"
title: "Let's Verify Step by Step"
authors: ["Hunter Lightman", "Vineet Kosaraju", "Yura Burda", "Harri Edwards", "Bowen Baker", "Teddy Lee", "Jan Leike", "John Schulman", "Ilya Sutskever", "Karl Cobbe"]
date: 2023-05-31
org: "OpenAI"
tags: [alignment, reward-modeling, reasoning, math, 2023]
upvotes: 11
---

# Let's Verify Step by Step

> The foundational **Process Reward Model (PRM)** paper. Proves that **step-level supervision** (process rewards) significantly outperforms **outcome-level supervision** (result-only rewards) for training reliable mathematical reasoning, and releases **PRM800K** — 800K step-level human feedback labels.

## Key Contributions
- **Process supervision > Outcome supervision**: Process reward models (PRMs) that evaluate each reasoning step substantially outperform outcome reward models (ORMs) that only check final answers
- **PRM800K**: Dataset of 800,000 step-level human labels (positive/negative/neutral) across 101,599 solution samples — the first large-scale process supervision dataset
- **Active learning**: Reduces human annotation cost by 2.6× by focusing labeling effort on the most informative solutions
- **78.2% on MATH** (best-of-1860) using PRM — the strongest result on this benchmark at time of publication
- Established the intellectual foundation for how modern reasoning models (DeepSeek-R1, o1) are trained and evaluated

## Method
### Setup
- **Generator**: GPT-4 base model fine-tuned to produce step-by-step solutions in newline-delimited format
- **Reward models**: Trained to score solutions and guide best-of-N selection
- All models fine-tuned from GPT-4 base (pre-RLHF)

### Outcome Reward Models (ORMs)
- Trained on (solution, correct/incorrect) labels
- Labels determined automatically by checking final answer
- Must implicitly learn where errors occur — difficult credit assignment

### Process Reward Models (PRMs)
- Trained on (step, positive/negative/neutral) labels from human annotators
- Each step scored independently given the solution prefix
- Final solution score: product of step-level probabilities (or minimum)
- Provides fine-grained feedback on exactly where reasoning goes wrong

### Data Collection (PRM800K)
- Human labelers annotate each step as:
  - **Positive**: Correct and well-reasoned
  - **Negative**: Contains an error
  - **Neutral**: Correct but routine/trivial
- Active learning: Use a preliminary PRM to select the most informative solutions for labeling
- 1,085,590 total step-level labels collected

### Evaluation
- **Best-of-N**: Generate N solutions, use reward model to select the best one
- Compare ORM vs PRM at various N (1 to 1860)
- PRM consistently selects better solutions, especially at large N

## Results
- **MATH (best-of-1860)**: PRM achieves **78.2%** vs ORM at **72.4%** — 5.8% absolute improvement
- **Active learning**: 2.6× reduction in annotation cost for equivalent PRM performance
- Performance gap is consistent across all difficulty levels (not just hard problems)
- **OOD generalization**: PRM trained on MATH generalizes well to AP Calculus (86.7%), AP Physics (50%), AP Chemistry (80%)
- PRM provides interpretable feedback — can visualize exactly which step caused errors

## Impact on Later Work
This paper's key ideas appear throughout modern reasoning model training:
- **DeepSeek-R1**: Uses step-level verification (rule-based process rewards) for RL training
- **OpenAI o1**: Reportedly built on PRM-guided search/verification
- **Math-Shepherd**: Extends PRM concept to automated process reward generation
- **GRPO**: Group-level rewards are conceptually related to outcome vs process distinction

## Connections
- **Builds on**: [[sources/instructgpt]] (RLHF framework), Chain-of-Thought prompting
- **Influenced**: [[sources/deepseek-r1]] (process-level verification), [[sources/deepseekmath]] (reward design), OpenAI o1
- **Key concepts**: [[concepts/process-reward-models]], [[concepts/rlhf]], [[concepts/scaling-laws]]
- **Organizations**: [[entities/orgs/openai]]
- **Dataset**: PRM800K (released on GitHub, 2.1K ⭐)

## Citation
> Lightman et al., "Let's Verify Step by Step," ICLR 2024, arXiv:2305.20050, 2023.
> https://huggingface.co/papers/2305.20050
