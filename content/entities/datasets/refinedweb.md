---
type: entity
category: dataset
tags: [pre-training, web-data]
---

# RefinedWeb

> A massive, high-quality web dataset created by aggressive filtering and deduplication of Common Crawl — proving that **web data alone** can outperform curated multi-source corpora.

## Overview
RefinedWeb challenged the assumption that training competitive LLMs requires carefully curated mixtures of books, papers, and code. By applying rigorous filtering and deduplication to Common Crawl alone, the resulting dataset produced models that outperformed those trained on The Pile.

## Key Details
- **Size**: ~5T tokens total; 600B tokens released publicly
- **Source**: Common Crawl (web data only)
- **Processing**: URL filtering → text extraction → language ID → quality filtering → dedup (exact + fuzzy)
- **Models trained**: Falcon family (7B, 40B, 180B)
- **HF Hub**: [tiiuae/falcon-refinedweb](https://huggingface.co/datasets/tiiuae/falcon-refinedweb)

## Influence
The RefinedWeb pipeline influenced subsequent data efforts including FineWeb (Hugging Face), which built on similar principles of aggressive web data filtering.

## Related Papers
- [[sources/refinedweb]] — RefinedWeb paper

## See Also
- [[entities/models/falcon]] — Falcon model family
- [[entities/orgs/tii]] — TII (creator)
- [[entities/datasets/fineweb]] — FineWeb (built on similar principles)
- [[concepts/pre-training]]
- [[concepts/scaling-laws]]
