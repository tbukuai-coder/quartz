---
type: source
arxiv_id: "2506.01732"
title: "Common Corpus: The Largest Collection of Ethical Data for LLM Pre-Training"
authors: ["Pierre-Carl Langlais", "Carlos Rosas Hinostroza", "Mattia Nee", "Catherine Arnett", "Pavel Chizhov", "Eliot Krzystof Jones", "Irène Girard", "David Mach", "Anastasia Stasenko", "Ivan P. Yamshchikov"]
date: 2025-06-03
org: "PleIAs / Common Corpus Consortium"
tags: [data, pre-training, open-science, multilingual, ethical-data, public-domain, 2025]
upvotes: 6
---

# Common Corpus: The Largest Collection of Ethical Data for LLM Pre-Training

> The largest open and compliant dataset for LLM pretraining — 1.99 trillion tokens across six collections (government, culture, science, web, code, semantic), with rigorous provenance tracking and public-domain focus.

## Key Contributions
- **Largest ethical pretraining corpus**: 1,998,647,168,282 tokens (nearly 2 trillion)
- **Fully open provenance**: Every document includes source URL, license, language, domain, and collection metadata
- **Six diverse collections**: Open Government, Open Culture, Open Science, Open Web, Open Code, Open Semantic
- **Multilingual**: Data in high- and low-resource languages, never machine-translated
- **Public domain majority**: Most data is in the public domain, with explicit license documentation
- **Open science infrastructure**: Released tools for data curation, cleaning, and evaluation
- **UNESCO-aligned**: Supports open science as a shared research infrastructure

## Method

### Six Collections

| Collection | Description | Key Sources |
|---|---|---|
| **Open Government** | Government documents, legislation, official publications | National archives, government portals |
| **Open Culture** | Cultural heritage, literature, historical texts | Libraries, museums, cultural institutions |
| **Open Science** | Scientific papers, preprints, research outputs | Open access journals, arXiv, etc. |
| **Open Web** | Web pages filtered for open licensing | Common Crawl with license filtering |
| **Open Code** | Source code repositories | GitHub with open licenses |
| **Open Semantic** | Structured knowledge, ontologies, linked data | Wikidata, DBpedia, etc. |

### Cleaning Pipeline
- **Segmentext**: Text segmentation from mixed-format documents
- **OCRoscope**: OCR error detection
- **OCRerrcr**: OCR error correction
- **OCRonos**: Advanced OCR correction
- **Celadon**: Toxicity detection and filtering
- **PII removal**: Personally identifiable information scrubbing

### Tokenization
- Uses PleIAs tokenizer trained on a representative subsample of Common Corpus
- Available at: `PleIAs/Pleias-350m-Preview`

## Results

### Scale and Diversity
- **Total tokens**: 1,998,647,168,282 (~2 trillion)
- **Languages**: At least 10B tokens for 9 languages; many more with smaller counts
- **Distribution**: Log-scaled across languages with 10,000+ documents each
- **Temporal span**: Documents spanning centuries (see timeline visualization in paper)

### Quality
- Extensive OCR error correction pipeline (4 specialized tools)
- Toxicity filtering (Celadon)
- PII removal
- Quality scoring and deduplication
- FastText language identification for accurate language tagging

## Connections
- Builds on: [[sources/fineweb|FineWeb]] (web data curation), [[sources/refinedweb|RefinedWeb]] (web filtering), [[sources/dolma|DOLMA]] (open data precedent), [[sources/common-pile|Common Pile]] (complementary open dataset)
- Cited by / Influenced: [[sources/apertus|Apertus]] (uses Common Corpus as part of its data mix)
- Related concepts: [[concepts/pre-training|Pre-training]], [[concepts/multilingual-models|Multilingual Models]], [[comparisons/pretraining-data|Pretraining Data Comparison]]
- Related datasets: [[entities/datasets/dolma|DOLMA]], [[entities/datasets/refinedweb|RefinedWeb]], [[entities/datasets/fineweb|FineWeb]], [[entities/datasets/the-stack|The Stack]]
- Related orgs: Part of the open science infrastructure movement alongside [[entities/orgs/allenai|AllenAI]] (DOLMA)

## Citation
> Langlais et al., "Common Corpus: The Largest Collection of Ethical Data for LLM Pre-Training," arXiv:2506.01732, 2025.
