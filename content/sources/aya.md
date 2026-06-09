---
type: source
arxiv_id: "2402.07827"
title: "Aya Model: An Instruction Finetuned Open-Access Multilingual Language Model"
authors: ["Ahmet Üstün", "Viraat Aryabumi", "et al."]
date: 2024-02-12
org: "Cohere For AI"
tags: [multilingual, instruction-tuning, open-models, 2024]
upvotes: 48
---

# Aya: Massively Multilingual Instruction-Tuned Model

> The most **multilingual open instruction model** — covering **101 languages** (50%+ lower-resourced), outperforming mT0 and BLOOMZ while serving double the number of languages. A community-driven effort from **Cohere For AI** with 3,000+ contributors across 119 countries.

## Key Contributions
- **101 languages**: More than double the language coverage of mT0/BLOOMZ, with 50%+ lower-resourced languages
- **Aya Dataset**: 204K human-curated instruction-response pairs across 65 languages
- **Aya Collection**: 44 datasets + templates for 114 languages (~513M instances)
- **Community-driven**: 3,000+ contributors from 119 countries via open annotation platform
- **Strong evaluation**: Win rates vs. mT0 and BLOOMZ across generative and discriminative tasks

## Model Family
| Model | Year | Base | Languages | Key Feature |
|---|---|---|---|---|
| Aya-101 | 2024 | mT5 (13B) | 101 | First massively multilingual instruct model |
| Aya-23 | 2024 | Command-R (8B/35B) | 23 | Focused quality on 23 languages |
| Aya-Expanse | 2024 | Custom (8B/32B) | 23 | SOTA multilingual, data arbitrage |

## Results
- Aya-101 outperforms mT0 (13B) and BLOOMZ (7.1B) on majority of tasks in covered languages
- Particularly strong on lower-resourced languages where alternatives have thin coverage
- Human evaluation shows clear preference over BLOOMZ across diverse language groups

## Significance
1. **Language equity**: First serious effort to bring instruction-following to 100+ languages
2. **Community model**: Largest multilingual data collection effort (3K contributors)
3. **Beyond English**: Challenged the English-centric bias of the instruction-tuning literature
4. **Cohere For AI**: Non-profit research lab within Cohere focused on open multilingual AI

## Connections
- Related: [[sources/bloom|BLOOM]] (earlier multilingual effort), [[concepts/multilingual-models]]
- Concepts: [[concepts/instruction-tuning]], [[concepts/multilingual-models]]
- Comparisons: [[comparisons/open-model-families]]

## Citation
> Üstün et al., "Aya Model: An Instruction Finetuned Open-Access Multilingual Language Model," arXiv:2402.07827, 2024.
