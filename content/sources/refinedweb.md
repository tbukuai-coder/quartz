---
type: source
arxiv_id: "2306.01116"
title: "The RefinedWeb Dataset for Falcon LLM: Outperforming Curated Corpora with Web Data, and Web Data Only"
authors: ["Guilherme Penedo", "Quentin Malartic", "Daniel Hesslow", "et al."]
date: 2023-06-01
org: "Technology Innovation Institute (TII)"
tags: [datasets, pre-training, data-quality, 2023]
upvotes: 44
---

# The RefinedWeb Dataset for Falcon LLM

> Demonstrated that **carefully filtered and deduplicated web data alone** can produce LLMs that outperform models trained on curated corpora (The Pile), challenging the assumption that high-quality data requires curation beyond web scraping.

## Key Contributions
- Created **RefinedWeb** — a massive, high-quality web dataset produced by aggressive filtering and deduplication of Common Crawl
- Showed that models trained **only on web data** outperform models trained on The Pile (a curated multi-source corpus)
- Released a 600B token extract of RefinedWeb publicly
- Provided a detailed, reproducible data processing pipeline
- Trained the **Falcon** family of models on this data

## Method
The RefinedWeb pipeline:
1. **URL filtering**: Remove adult, spam, and low-quality domains
2. **Text extraction**: Careful HTML-to-text conversion (trafilatura)
3. **Language identification**: Filter for English (or target language)
4. **Quality filtering**: Heuristic rules (document length, character ratios, repetition)
5. **Deduplication**: Exact dedup (URL + content hash) + fuzzy dedup (MinHash LSH)
6. **No curation by source type** — purely web data, no books/papers/code specifically

Key finding: the quality gap between web data and curated data is primarily about **filtering and deduplication quality**, not about source diversity.

## Results
- Falcon models trained on RefinedWeb outperform models trained on The Pile at equivalent scale
- Falcon-40B was the top-performing open model on the Open LLM Leaderboard at release
- RefinedWeb contains ~5T high-quality tokens (600B released publicly)

## Connections
- **Influenced**: [[sources/smollm2]] (FineWeb-Edu builds on similar philosophy), data pipeline methodology across the ecosystem
- **Key concepts**: [[concepts/pre-training]], [[concepts/scaling-laws]]
- **Datasets**: [[entities/datasets/refinedweb]]

## Citation
> Penedo et al., "The RefinedWeb Dataset for Falcon LLM," arXiv:2306.01116, 2023.
> https://huggingface.co/papers/2306.01116
