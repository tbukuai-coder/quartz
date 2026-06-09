---
type: source
arxiv_id: "2402.00159"
title: "Dolma: an Open Corpus of Three Trillion Tokens for Language Model Pretraining Research"
authors: ["Luca Soldaini", "Rodney Kinney", "Akshita Bhagia", "et al."]
date: 2024-01-31
org: "AllenAI"
tags: [data-curation, pre-training, open-science, 2024]
upvotes: 65
---

# Dolma

> A **3 trillion token open English corpus** from AllenAI — the pretraining dataset for [[entities/models/olmo|OLMo]]. Built from a diverse mixture of web content, academic papers, code, books, social media, and encyclopedic materials. Released with an open-source **data curation toolkit** enabling reproduction and experimentation.

## Key Contributions
- **3T token open corpus**: Largest fully documented and open pretraining dataset at release
- **Open curation toolkit**: dolma toolkit enables researchers to reproduce and modify the pipeline
- **Extensive ablations**: Systematic experiments on filtering, deduplication, mixing, and decontamination
- **Multi-source diversity**: Web (Common Crawl), code (The Stack), academic (peS2o), books, Wikipedia, Reddit
- **Used to train OLMo**: Direct evidence that the dataset produces competitive models

## Composition
| Source | Tokens | % | Description |
|---|---|---|---|
| Common Crawl | 2.13T | 71% | Web content (5 snapshots, deduplicated, quality-filtered) |
| The Stack | 411B | 14% | Permissively licensed code from GitHub |
| C4 | 190B | 6% | Curated web content |
| Reddit | 89B | 3% | Conversational forums (threaded) |
| peS2o | 70B | 2% | Academic papers (Semantic Scholar) |
| Project Gutenberg | 5.4B | 0.2% | Public domain books |
| Wikipedia + Wikibooks | 3.7B | 0.1% | Encyclopedic knowledge |

## Pipeline
```
Raw sources → Language ID (English) → Quality filtering → Deduplication → PII removal → Decontamination → Mixing → Dolma
```

### Key Design Decisions
1. **URL-based deduplication**: Exact URL dedup across CC snapshots + paragraph-level dedup within
2. **Quality filtering**: Combination of heuristic (length, repetition) and classifier-based filters
3. **FastText language ID**: English-only filtering with dialect fairness analysis
4. **Toxicity filtering**: Jigsaw classifier with dialect bias analysis
5. **Benchmark decontamination**: Removed training data matching common benchmarks
6. **No upsampling**: Used natural frequency of each source (following Falcon's approach)

## Ablation Findings
- **Deduplication is critical**: Paragraph-level dedup significantly improves downstream performance
- **Quality filtering has mixed effects**: Aggressive filtering helps knowledge benchmarks but can hurt diversity
- **Toxicity filtering**: Modest impact on model quality; classifier has dialectal biases
- **Multi-source mixing**: Upsampling high-quality sources (Wikipedia, books) helps some benchmarks but not all

## Impact
- Used to train all OLMo models (v1, v2, v3)
- OLMoE-Mix builds on Dolma with additional sources
- Dolma toolkit adopted by other open-data projects
- Enabled systematic study of how pretraining data affects model capabilities
- 1.5K GitHub stars for the dolma repository

## Connections
- Used by: [[sources/olmo|OLMo]], [[sources/olmo-2|OLMo 2]], [[sources/olmo-3|OLMo 3]], [[sources/olmoe|OLMoE]]
- Entity: [[entities/datasets/dolma]]
- Org: [[entities/orgs/allenai|AllenAI]]
- Related: [[entities/datasets/refinedweb]], [[entities/datasets/fineweb]], [[entities/datasets/redpajama]]
- Concepts: [[concepts/pre-training]]
- Comparisons: [[comparisons/pretraining-data]]

## Citation
> Soldaini et al., "Dolma: an Open Corpus of Three Trillion Tokens for Language Model Pretraining Research," arXiv:2402.00159, 2024.
