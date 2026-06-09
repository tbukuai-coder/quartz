---
type: source
arxiv_id: "2605.06643"
title: "Are We Making Progress in Multimodal Domain Generalization? A Comprehensive Benchmark Study"
authors: ["Hao Dong", "Hongzhao Li", "Shupan Li", "Muhammad Haris Khan", "Eleni Chatzi", "Olga Fink"]
date: 2026-05
tags: [multimodal, domain-generalization, benchmark, robustness, action-recognition, fault-diagnosis, sentiment-analysis]
upvotes: 1
---

# Are We Making Progress in Multimodal Domain Generalization? A Comprehensive Benchmark Study

> MMDG-Bench presents a unified benchmark for multimodal domain generalization that standardizes evaluation across diverse tasks and modalities, revealing limited performance gains and significant robustness challenges.

## Key Contributions
- Identifies fragmentation in multimodal domain generalization (MMDG) research with inconsistent evaluation protocols
- Introduces MMDG-Bench, a unified benchmark standardizing evaluation across datasets, modality configurations, and settings
- Covers multiple domains: action recognition, mechanical fault diagnosis, sentiment analysis, corruption robustness
- Includes missing-modality generalization and out-of-distribution detection
- Reveals that reported performance gains may be artifacts of inconsistent protocols rather than genuine algorithmic progress

## Method
MMDG-Bench standardizes:
1. **Datasets**: Multiple multimodal datasets with domain shifts
2. **Modality configurations**: Audio-visual, text-visual, text-audio, etc.
3. **Evaluation settings**: Cross-domain action recognition, fault diagnosis, sentiment analysis
4. **Robustness tests**: Corruption robustness, missing-modality generalization
5. **OOD detection**: Out-of-distribution detection performance
6. **ERM baseline**: Empirical Risk Minimization as the fundamental baseline for fair comparison

## Results
- Limited genuine performance gains when evaluated under standardized protocols
- Significant robustness challenges remain in multimodal domain generalization
- Many reported improvements disappear under fair comparison with consistent settings

## Datasets Used
- Multiple multimodal domain generalization datasets (action recognition, fault diagnosis, sentiment analysis)

## Models Released
- GitHub: https://github.com/lihongzhao99/MMDG_Benchmark (9 stars)

## Connections
- Related: [[sources/cambrian]] — vision-centric MLLM evaluation
- Related: [[sources/aya-vision]] — multilingual multimodal robustness
- Related concept: [[concepts/multimodal-models]], [[concepts/llm-evaluation]]

## Citation
> Dong et al., "Are We Making Progress in Multimodal Domain Generalization? A Comprehensive Benchmark Study," arXiv:2605.06643, 2026.
