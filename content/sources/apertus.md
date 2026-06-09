---
type: source
arxiv_id: "2509.14233"
title: "Apertus: Democratizing Open and Compliant LLMs for Global Language Environments"
authors: ["Alejandro Hernández-Cano", "Alexander Hägele", "Allen Hao Huang", "Angelika Romanou", "Antoni-Joan Solergibert", "Barna Pasztor", "Bettina Messmer", "Dhia Garbaya", "Eduard Frank Ďurech", "Ido Hakimi"]
date: 2025-09-22
org: "Swiss AI Center / EPFL / Cohere For AI / PleIAs"
tags: [open-science, multilingual, pre-training, data-compliance, goldfish-objective, 2025]
upvotes: 18
---

# Apertus: Democratizing Open and Compliant LLMs for Global Language Environments

> A fully open suite of LLMs pretrained exclusively on openly available data with robots.txt compliance, Goldfish objective for memorization suppression, and 15T tokens across 1800+ languages — released with all scientific artifacts under permissive licenses.

## Key Contributions
- **Data compliance by design**: Pretrained exclusively on openly available data, retroactively respecting robots.txt exclusions, filtering non-permissive/toxic/PII content
- **Goldfish objective**: Suppresses verbatim recall of training data while retaining downstream task performance, mitigating memorization risks
- **Multilingual expansion**: 15T tokens from 1800+ languages, ~40% non-English — largest multilingual open pretraining corpus to date
- **Full artifact release**: Model weights, data preparation scripts, checkpoints, evaluation suites, and training code under permissive license
- **Competitive performance**: 8B and 70B models approach SOTA among fully open models on multilingual benchmarks

## Method

### Data Curation Pipeline
Apertus implements a rigorous compliance pipeline:
1. **Source filtering**: Only openly available data; robots.txt exclusions retroactively applied
2. **Content filtering**: Non-permissive content, toxic material, and PII removal
3. **License verification**: All data sources verified for open licensing
4. **Quality scoring**: Multi-stage filtering with quality heuristics

### Goldfish Objective
During pretraining, the Goldfish objective strongly suppresses verbatim recall of training sequences while maintaining generalization. This is achieved by modifying the loss function to downweight exact n-gram matches, reducing risks of:
- Copyright infringement via memorization
- Privacy leakage from PII-containing text
- Benchmark contamination from test-set overlap

### Training
- **Data**: 15T tokens, ~40% non-English, 1800+ languages
- **Architecture**: Standard transformer (8B and 70B parameters)
- **Post-training**: SFT + DPO alignment pipeline
- **License**: All artifacts permissively licensed

## Results

| Model | Size | Multilingual Benchmarks | Open-Weight Counterparts |
|---|---|---|---|
| Apertus-8B | 8B | Approaches SOTA among fully open | Competitive with open-weight 7B models |
| Apertus-70B | 70B | SOTA among fully open | Rivals or surpasses open-weight 70B models |

- Strong performance on multilingual benchmarks across high- and low-resource languages
- Verbatim memorization significantly reduced compared to baseline models
- GitHub: [swiss-ai/apertus-tech-report](https://github.com/swiss-ai/apertus-tech-report) (133 ⭐)

## Datasets Used
- Curated multilingual web corpus (openly licensed)
- Open government, open culture, open science collections
- Multiple language-specific open datasets

## Models Released
- **swiss-ai/Apertus-8B-2509** — Base model (8B)
- **swiss-ai/Apertus-8B-Instruct-2509** — Instruct-tuned (8B)
- **swiss-ai/Apertus-70B-2509** — Base model (70B)
- **swiss-ai/Apertus-70B-Instruct-2509** — Instruct-tuned (70B)

## Connections
- Builds on: [[sources/fineweb2|FineWeb2]] (multilingual data curation), [[sources/common-pile|Common Pile]] (open data philosophy), [[sources/olmo|OLMo]] (fully open model precedent)
- Cited by / Influenced: Part of the growing fully-open model movement alongside OLMo
- Related concepts: [[concepts/pre-training|Pre-training]], [[concepts/multilingual-models|Multilingual Models]], [[comparisons/open-science-vs-open-weight|Open-Science vs Open-Weight]]
- Related orgs: [[entities/orgs/cohere|Cohere For AI]] (multilingual expertise), [[entities/orgs/allenai|AllenAI]] (OLMo fully-open precedent)

## Citation
> Hernández-Cano et al., "Apertus: Democratizing Open and Compliant LLMs for Global Language Environments," arXiv:2509.14233, 2025.
