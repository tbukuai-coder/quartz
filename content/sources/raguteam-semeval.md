---
type: source
arxiv_id: "2605.04523"
title: "RaguTeam at SemEval-2026 Task 8: Meno and Friends in a Judge-Orchestrated LLM Ensemble for Faithful Multi-Turn Response Generation"
authors: ["Ivan Bondarenko", "Roman Derunets", "Oleg Sedukhin", "Mikhail Komarov", "Ivan Chernov", "Mikhail Kulakov"]
date: 2026-05
tags: [ensemble, prompting, llm, judge-selection, semeval, multi-turn, rag]
upvotes: 25
---

# RaguTeam at SemEval-2026 Task 8: Meno and Friends in a Judge-Orchestrated LLM Ensemble

> A heterogeneous ensemble of seven LLMs with dual prompting strategies achieved 1st place in SemEval-2026 Task 8 (MTRAGEval) through GPT-4o-mini judge selection, demonstrating that diversity in model families, scales, and prompting is essential.

## Key Contributions
- Won 1st place (out of 26 teams) in SemEval-2026 Task 8: MTRAGEval (Multi-Turn Response Generation with Reference Passages)
- Uses a heterogeneous ensemble of **seven LLMs** with **two prompting variants** per model (14 total candidates)
- Employs a **GPT-4o-mini judge** to select the best candidate per instance
- Achieved conditioned harmonic mean of 0.7827, outperforming the strongest baseline (gpt-oss-120b at 0.6390)
- Ablations show that **diversity in model families, scales, and prompting strategies is essential** for ensemble performance

## Method
The Meno and Friends system:
1. **Heterogeneous model selection**: Seven different LLMs from diverse families and scales
2. **Dual prompting**: Two distinct prompt templates per model to increase response diversity
3. **Candidate generation**: 14 candidate responses per query (7 models × 2 prompts)
4. **Judge selection**: GPT-4o-mini evaluates all 14 candidates and selects the best one based on faithfulness to reference passages
5. **Conditioned harmonic mean**: The final metric conditions on the judge's confidence in its selection

## Results
- **1st place** out of 26 teams in SemEval-2026 Task 8
- Conditioned harmonic mean: **0.7827** (baseline gpt-oss-120b: 0.6390)
- Ablations confirm diversity across model families, parameter scales, and prompting strategies is critical
- Single large model cannot match the ensemble performance even with optimized prompting

## Datasets Used
- SemEval-2026 Task 8: MTRAGEval dataset

## Models Released
- GitHub: https://github.com/RaguTeam/ragu_mtrag_semeval (0 stars)

## Connections
- Related: [[sources/mixture-of-agents]] — combining multiple LLM outputs
- Related: [[sources/malt]] — multi-agent LLM training
- Related: [[sources/zephyr]] — AI feedback for alignment
- Related concept: [[concepts/agents]], ensemble methods

## Citation
> Bondarenko et al., "RaguTeam at SemEval-2026 Task 8: Meno and Friends in a Judge-Orchestrated LLM Ensemble for Faithful Multi-Turn Response Generation," arXiv:2605.04523, 2026.
