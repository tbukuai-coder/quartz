---
type: source
arxiv_id: "2406.17557"
title: "The FineWeb Datasets: Decanting the Web for the Finest Text Data at Scale"
authors: ["Guilherme Penedo", "Hynek Kydlíček", "Loubna Ben allal", "Anton Lozhkov", "Margaret Mitchell", "Colin Raffel", "Leandro Von Werra", "Thomas Wolf"]
date: 2024-06-25
org: "Hugging Face"
tags: [pre-training, data-curation, 2024]
upvotes: 102
---

# FineWeb: Decanting the Web for the Finest Text Data at Scale

> Introduces **FineWeb** (15T tokens from 96 Common Crawl snapshots) and **FineWeb-Edu** (1.3T tokens of educational content), open pretraining datasets that produce better LLMs than all other publicly available datasets — with fully documented, ablated curation pipeline.

## Key Contributions
- **FineWeb**: 15-trillion token English dataset from 96 Common Crawl snapshots — the largest high-quality open pretraining dataset
- **FineWeb-Edu**: 1.3T token subset filtered for educational content using an LLM-based quality classifier, yielding dramatic improvements on knowledge benchmarks
- **Comprehensive ablation methodology**: Systematic "data ablation" framework — train identical 1.71B models on 28B tokens from each pipeline variant to compare design choices
- **Open everything**: Dataset, curation code, all ablation models, and educational quality classifier released openly
- Demonstrated that a single carefully designed pipeline (text extraction → base filtering → deduplication → heuristic filtering → educational filtering) beats all prior open datasets

## Method
### FineWeb Pipeline
1. **Text extraction**: trafilatura on WARC files (not WET) — 2–3% benchmark improvement over WET-based extraction
2. **Base filtering**: URL blocklist, fastText language ID, quality heuristics from [[sources/refinedweb|RefinedWeb]]
3. **Deduplication**: Independent MinHash per snapshot (5-grams, 112 hash functions) — individual dedup outperforms global dedup
4. **Custom heuristic filters**: Systematic filter design using 50+ document statistics, threshold tuning via ablation models
5. **C4 filters**: Adapted subset of C4's line-level filtering rules, adding ~0.5% benchmark improvement

### FineWeb-Edu
- Train a quality classifier (Llama-3-70B annotations → lightweight classifier) to score documents 0–5 on educational value
- Filter FineWeb keeping only documents scoring ≥ 3
- Result: 1.3T tokens that dramatically outperform full FineWeb on knowledge-intensive benchmarks (MMLU, ARC, OpenBookQA)
- Topic analysis shows upsampling of education, science, history; downsampling of entertainment, commerce

### Ablation Framework
- 1.71B parameter Llama-architecture models
- 28B tokens for quick ablations, 350B tokens for final validation
- Same architecture, optimizer, hyperparameters — only data varies
- Evaluation on aggregate of HellaSwag, ARC, MMLU, OpenBookQA, PIQA, Winogrande, BoolQ, SciQ, LAMBADA

## Results
- **FineWeb** outperforms RefinedWeb, C4, Dolma, RedPajama v1/v2 on aggregate benchmarks
- **FineWeb-Edu** outperforms all open datasets on knowledge-intensive benchmarks by large margins
- Used as pretraining data for [[sources/smollm2|SmolLM2]] and many community models
- Key ablation findings:
  - WARC → trafilatura beats WET extraction (+2–3%)
  - Independent per-snapshot dedup beats global dedup
  - Custom heuristic filters add incremental but consistent gains
  - Educational filtering is the single largest quality lever

## Datasets Released
- **FineWeb**: 15T tokens — `HuggingFaceFW/fineweb`
- **FineWeb-Edu**: 1.3T tokens — `HuggingFaceFW/fineweb-edu`
- **FineWeb-Edu-score-2**: 5.4T tokens (threshold ≥ 2) — `HuggingFaceFW/fineweb-edu-score-2`

## Connections
- **Builds on**: [[sources/refinedweb]] (base filtering approach), [[sources/scaling-data-constrained]] (data quality matters)
- **Used by**: [[sources/smollm2]] (pretraining data)
- **Key concepts**: [[concepts/pre-training]], [[concepts/scaling-laws]]
- **Organizations**: [[entities/orgs/huggingface]]
- **Related datasets**: [[entities/datasets/refinedweb]], [[entities/datasets/fineweb]]

## Citation
> Penedo et al., "The FineWeb Datasets: Decanting the Web for the Finest Text Data at Scale," arXiv:2406.17557, 2024.
> https://huggingface.co/papers/2406.17557
