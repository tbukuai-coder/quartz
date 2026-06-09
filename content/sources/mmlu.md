---
type: source
arxiv_id: "2009.03300"
title: "Measuring Massive Multitask Language Understanding"
authors: ["Dan Hendrycks", "Collin Burns", "Steven Basart", "Andy Zou", "Mantas Mazeika", "Dawn Song", "Jacob Steinhardt"]
date: 2020-09-07
org: "UC Berkeley"
tags: [evaluation, benchmark, foundational]
upvotes: 3
---

# MMLU — Measuring Massive Multitask Language Understanding

> The universal benchmark for evaluating LLM knowledge and reasoning across 57 tasks — cited on virtually every model card and leaderboard in the HF ecosystem.

## Key Contributions
- **57-task benchmark** covering STEM, humanities, social sciences, law, medicine, and professional domains
- **Standard evaluation metric** that became the de facto measure of LLM progress — from GPT-3's 43% to modern models scoring 90%+
- **Revealed scaling dynamics**: Only the largest GPT-3 (175B) improved meaningfully over random chance; smaller models were near-random
- **Identified blind spots**: Models had near-random accuracy on socially important subjects (morality, law) even when strong on STEM

## Method
The test consists of multiple-choice questions (4 options each) from 57 subjects at varying difficulty levels:
- **Humanities**: philosophy, history, law, ethics, literature
- **Social Sciences**: economics, psychology, sociology, political science, geography
- **STEM**: physics, chemistry, biology, computer science, mathematics, engineering
- **Other**: professional medicine, clinical knowledge, business, accounting

Questions range from elementary to advanced professional level. Models are evaluated with few-shot prompting (0-shot and 5-shot). Accuracy is averaged across all 57 tasks.

## Results
- **GPT-3 175B (5-shot)**: 43.9% average (vs. 25% random)
- Three smaller GPT-3 models: near-random (~25%)
- UnifiedQA: 48.9% (best fine-tuned model at time of publication)
- **Today's frontier**: GPT-4o, Claude 3.5, Qwen3-235B score 85–90%+
- Model performance is "lopsided" — strong on some subjects, near-random on others
- Models frequently don't know when they're wrong (poor calibration)

## Impact on the Ecosystem
MMLU became the **primary yardstick** for the open-source LLM leaderboard era:
- HF Open LLM Leaderboard used MMLU as a core benchmark
- Every model card in the wiki cites MMLU scores
- Spawned successors: MMLU-Pro (harder), MMLU-Redux (decontaminated)

## Datasets Used
- Questions sourced from professional exams, academic tests, and standardized assessments
- **MMLU dataset on HF Hub**: `cais/mmlu` — widely used for evaluation

## Connections
- Evaluated by: Every model in this wiki — [[sources/llama|LLaMA]], [[sources/mistral-7b|Mistral]], [[sources/qwen25|Qwen2.5]], [[sources/phi-4|Phi-4]], etc.
- Related: [[concepts/scaling-laws|Scaling Laws]] (MMLU reveals scaling thresholds)
- Concept: [[concepts/llm-evaluation|LLM Evaluation & Benchmarks]]

## Citation
> Hendrycks et al., "Measuring Massive Multitask Language Understanding," ICLR 2021, arXiv:2009.03300.
