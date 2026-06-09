---
type: source
arxiv_id: "2408.03314"
title: "Scaling LLM Test-Time Compute Optimally can be More Effective than Scaling Model Parameters"
authors: ["Charlie Snell", "Jaehoon Lee", "Kelvin Xu", "Aviral Kumar"]
date: 2024-08-06
org: "UC Berkeley / Google DeepMind"
tags: [reasoning, test-time-scaling, inference, scaling-laws, process-reward-models, 2024]
upvotes: 65
---

# Scaling LLM Test-Time Compute

> A theoretical and empirical framework showing that compute-optimal test-time scaling (searching with verifiers + adaptive revision) can make a small model outperform one 14× larger.

## Key Contributions
- **Compute-optimal test-time strategies**: Derives when to use best-of-N sampling vs. sequential revision vs. beam search depending on prompt difficulty
- **Difficulty-dependent effectiveness**: Test-time compute helps most on "medium-difficulty" prompts; too easy = wasteful, too hard = futile
- **14× parameter-equivalent gain**: On appropriate problems, a small model with optimal test-time compute matches a 14× larger model
- **Unified framework**: Views all test-time strategies through the lens of modifying the model's predicted distribution via a proposer + verifier

## Method
Two primary mechanisms analyzed:
1. **Search against process verifiers (PRMs)**:
   - Best-of-N: Generate N solutions, use PRM to pick the best — scales with sqrt(N)
   - Beam search: Step-level search guided by PRM scores — more compute-efficient
   - PRM aggregation: Product of step scores works best (not min, not last)
2. **Adaptive proposal distribution (revision)**:
   - Model iteratively revises its own answers — sequential test-time scaling
   - Revision model trained on synthetic data: correct answers with N random prior attempts prepended
   - More sample-efficient than parallel sampling on hard problems

**Compute-optimal strategy**: Allocate compute based on estimated prompt difficulty:
- Easy prompts: best-of-N (cheap, diminishing returns quickly)
- Medium prompts: beam search or revision (most benefit)
- Hard prompts: revision chains (sequential deepening)

## Results
- Compute-optimal strategy is **4× more efficient** than best-of-N baseline
- On FLOPs-matched evaluation: smaller model + test-time compute > 14× larger model (on "medium" difficulty)
- PRM beam search outperforms best-of-N at same compute budget
- Revision improves with more iterations on hard problems but plateaus on easy ones
- Process verifiers (PRMs) significantly outperform outcome verifiers (ORMs)
- Results on MATH benchmark using PaLM 2-S* models

## Datasets Used
- MATH benchmark (competition math)
- PRM800K (process reward model training data from [[sources/lets-verify-step-by-step|Let's Verify Step by Step]])

## Connections
- Builds on: [[sources/lets-verify-step-by-step|Let's Verify Step by Step]] (PRM concept + PRM800K data)
- Enables: [[sources/deepseek-r1|DeepSeek-R1]], [[sources/s1|s1]], [[sources/kimi-k15|Kimi k1.5]] (practical reasoning models)
- Related: [[sources/open-reasoner-zero|Open-Reasoner-Zero]] (RL-based test-time scaling)
- Concepts: [[concepts/test-time-compute|Test-Time Compute Scaling]], [[concepts/process-reward-models|Process Reward Models]], [[concepts/scaling-laws|Scaling Laws]]
- Code: HuggingFace `search-and-learn` repository

## Citation
> Snell et al., "Scaling LLM Test-Time Compute Optimally can be More Effective than Scaling Model Parameters," arXiv:2408.03314, 2024.
