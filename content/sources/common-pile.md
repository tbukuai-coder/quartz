---
type: source
arxiv_id: "2506.05209"
title: "The Common Pile v0.1: An 8TB Dataset of Public Domain and Openly Licensed Text"
authors: ["Nikhil Kandpal", "Brian Lester", "Colin Raffel", "Stella Biderman", "Various"]
date: 2025-06-05
org: "EleutherAI / Various"
tags: [data, pre-training, open-science, licensing, 2025]
upvotes: 61
---

# The Common Pile v0.1

> An 8TB dataset of exclusively public domain and openly licensed text — the first pretraining corpus large enough to train competitive LLMs while fully respecting intellectual property rights. 254 GitHub ⭐.

## Key Contributions
- **8TB of openly licensed text** — largest rights-cleared pretraining dataset
- Trains **competitive 7B LLMs** — proves you don't need unlicensed data for good models
- Addresses **IP concerns**: all data is public domain, CC-BY, CC-BY-SA, or similarly licensed
- Curated from diverse sources: government documents, scientific papers, books, code, etc.
- Released with **training checkpoints** and mixture recipes

## Data Sources
- Public domain books (Project Gutenberg, Internet Archive)
- Government documents (US, EU, etc.)
- CC-licensed web content
- Permissively licensed code
- Scientific papers (arXiv, PubMed OA)
- Wikipedia and Wikidata

## Results
- 7B models trained on Common Pile competitive with models trained on unlicensed data
- Performance gap is narrowing — rights-cleared training is increasingly viable
- Models released as Llama-architecture checkpoints

## Connections
- **From**: [[entities/orgs/eleutherai|EleutherAI]] (continuing The Pile's legacy)
- **Related**: [[entities/datasets/the-stack|The Stack]] (permissive code), [[sources/fineweb|FineWeb]] (web-filtered, not rights-cleared)
- **Complements**: [[sources/fineweb2|FineWeb2]] (multilingual pipeline) — Common Pile focuses on licensing
- **Concept**: [[concepts/pre-training|Pre-training]], [[concepts/data-mixing|Data Mixing]]
- **Comparison**: [[comparisons/pretraining-data|Pretraining Data]], [[comparisons/open-science-vs-open-weight|Open Science]]

## Citation
> Kandpal et al., "The Common Pile v0.1: An 8TB Dataset of Public Domain and Openly Licensed Text," arXiv:2506.05209, 2025.
