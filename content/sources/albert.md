---
type: source
arxiv_id: "1909.11942"
title: "ALBERT: A Lite BERT for Self-supervised Learning of Language Representations"
authors: ["Zhenzhong Lan", "Mingda Chen", "Sebastian Goodman", "et al."]
date: 2019-09-26
org: "Google / Toyota"
tags: [foundational, encoder, efficiency, nlp]
upvotes: 1
---

# ALBERT: A Lite BERT

> Introduced **parameter reduction techniques** for BERT — **factorized embedding** and **cross-layer parameter sharing** — producing models 18× smaller than BERT-Large with comparable or better performance. ALBERT's factorized embeddings became standard practice in later models.

## Key Contributions
- **Factorized embedding**: Decompose large vocabulary embedding (V×H) into two smaller matrices (V×E and E×H) — massive parameter savings
- **Cross-layer parameter sharing**: Share parameters across transformer layers — further size reduction
- **Sentence Order Prediction (SOP)**: Replaced BERT's NSP with harder SOP task — improved multi-sentence understanding
- **ALBERT-xxlarge**: With just 12M unique parameters, matches BERT-Large (334M) on most benchmarks

## Results
| Model | Params | MNLI | SQuAD 2.0 | RACE |
|---|---|---|---|---|
| BERT-Large | 334M | 86.6 | 81.8 | 72.0 |
| **ALBERT-xxlarge** | **12M unique** | **90.8** | **88.1** | **86.5** |

18× fewer unique parameters, better results.

## Impact
- **Factorized embeddings** adopted by later efficient models
- Demonstrated that parameter sharing is viable at scale
- Influenced [[sources/distilbert|DistilBERT]] and other compression approaches
- Still available on HF Hub as lightweight encoder option

## Connections
- Builds on: [[sources/bert|BERT]]
- Related: [[sources/distilbert|DistilBERT]], [[concepts/distillation]]
- Org: [[entities/orgs/google|Google]]

## Citation
> Lan et al., "ALBERT: A Lite BERT for Self-supervised Learning of Language Representations," ICLR 2020, arXiv:1909.11942.
