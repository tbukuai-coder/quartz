---
type: source
arxiv_id: "2207.04672"
title: "No Language Left Behind: Scaling Human-Centered Machine Translation"
authors: ["NLLB Team", "Marta R. Costa-jussà", "James Cross"]
date: 2022-07-11
org: "Meta AI"
tags: [multilingual, translation, moe, foundational, 2022]
upvotes: 3
---

# NLLB (No Language Left Behind)

> Meta's massive multilingual translation system covering 200 languages using a Sparsely Gated MoE model, improving low-resource language translation by 44% BLEU.

## Key Contributions
- Built **NLLB-200**: a single translation model covering **200 languages** (including many low-resource)
- Used **Sparsely Gated Mixture of Experts** (54B total params) for efficient multilingual coverage
- Improved low-resource language translation by **44% BLEU** relative to prior SOTA
- Created **FLORES-200**: a multilingual benchmark covering 200 languages with human translations
- Developed safety measures including toxicity detection across all supported languages
- Released as fully open-source — one of the most downloaded models on HF Hub

## Method
NLLB uses a standard encoder-decoder architecture (like mBART) augmented with **Sparse MoE layers**. Key innovations:
- **Data mining**: Developed LASER3 and stopes tools for mining parallel sentences from web data
- **Conditional compute**: MoE allows scaling to 200 languages without proportional inference cost
- **Toxicity detection**: Built detectors for all 200 languages to prevent harmful translations
- Multiple model sizes: 600M (dense), 1.3B (dense), 3.3B (MoE), 54B (MoE)

## Results
- **FLORES-200**: NLLB-54B achieves SOTA on most translation pairs
- **Low-resource improvement**: 44% average BLEU improvement for the lowest-resource languages
- **Scale**: 40K+ translation directions (200 × 200 languages)
- **NLLB-200-distilled-600M**: Most downloaded translation model on HF Hub (100M+ downloads)

## Models Released
- NLLB-200 (600M, 1.3B, 3.3B, 54B) — all open weights

## Connections
- **Builds on**: mBART (multilingual encoder-decoder), LASER (parallel sentence mining)
- **Related**: [[sources/aya|Aya]] (multilingual instruction-following), [[concepts/multilingual-models|Multilingual Models]]
- **Architecture**: [[concepts/mixture-of-experts|Mixture of Experts]] (sparse gating)
- **Org**: [[entities/orgs/meta|Meta AI]]
- **Impact**: One of the most downloaded open models, enabling translation for 200 languages

## Citation
> NLLB Team, "No Language Left Behind: Scaling Human-Centered Machine Translation," arXiv:2207.04672, 2022.
