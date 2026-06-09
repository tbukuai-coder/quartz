---
type: source
arxiv_id: "2605.12882"
title: "CiteVQA: Benchmarking Evidence Attribution for Trustworthy Document Intelligence"
authors: ["Dongsheng Ma", "Jiayu Li", "Zhengren Wang", "Yijie Wang", "Jiahao Kong", "Weijun Zeng", "Jutao Xiao", "Jie Yang", "Wentao Zhang", "Bin Wang"]
date: 2026-05-18
org: "OpenDataLab / Shanghai AI Lab"
tags: [benchmark, vlm, document-understanding, evaluation, 2026]
upvotes: 269
---

# CiteVQA: Benchmarking Evidence Attribution for Trustworthy Document Intelligence

> First benchmark that jointly evaluates answer accuracy and evidence attribution (bounding-box citations) in document VQA, revealing widespread attribution hallucinations.

## Key Contributions
- Introduces **CiteVQA benchmark**: evaluates both answer correctness and correct citation of supporting evidence regions in documents
- Defines **Strict Attributed Accuracy (SAA)**: a metric requiring both correct answer and correct source-region grounding
- Reveals **Attribution Hallucination**: models frequently arrive at correct answers while grounding them in wrong passages — a critical risk in law, finance, and medicine
- Provides cross-domain evaluation spanning legal, financial, medical, and scientific documents
- Masking ablation studies show current models can score well without truly reading the cited region

## Method
CiteVQA requires models to output (answer, bounding-box-citation) pairs for document questions. Expert review validates ground-truth annotations. Models are evaluated on joint answer+attribution accuracy, with masking ablations exposing shortcut behavior.

## Results
- Leading MLLMs show significant gap between answer accuracy and attribution accuracy
- Attribution hallucination rates exceed 40% for some frontier models
- Masking ablations confirm models can maintain accuracy even when cited regions are occluded

## Connections
- Builds on: [[sources/llava]], [[concepts/vision-language-models]], [[concepts/llm-evaluation]]
- Related: [[sources/oscar-vlm]], [[sources/first-token-knows]], [[concepts/llm-safety]]
- Relevant to: [[entities/orgs/shanghai-ai-lab]]

## Citation
> Ma et al., "CiteVQA: Benchmarking Evidence Attribution for Trustworthy Document Intelligence," arXiv:2605.12882, 2026.
