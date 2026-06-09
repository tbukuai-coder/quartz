---
type: source
arxiv_id: "2305.16264"
title: "Scaling Data-Constrained Language Models"
authors: ["Niklas Muennighoff", "Alexander M. Rush", "Boaz Barak", "et al."]
date: 2023-05-25
org: "Hugging Face / Harvard"
tags: [scaling-laws, data, pre-training, 2023]
upvotes: 16
---

# Scaling Data-Constrained Language Models

> Investigated what happens when **data runs out** during LLM training — finding that data can be repeated up to ~4× with diminishing but positive returns, and providing new scaling laws for data-constrained regimes.

## Key Contributions
- Established **scaling laws for data repetition**: value of additional epochs follows a predictable decay
- Showed data can be repeated up to **~4 epochs** before returns become negligible
- Found that **additional compute** (larger models) can partially compensate for limited data
- Discovered that **code data** is uniquely valuable — mixing in code improves general performance even for non-code tasks
- Provided practical guidance: filter aggressively rather than repeat low-quality data

## Method
- Ran a massive experimental grid: varied model size (up to 9B params), dataset size, and repetition count
- Training runs up to 900B tokens across 400+ experiments
- Fitted scaling laws of the form: `L(N, D, R) = E + A/N^α + B/D^β + C·f(R)`
- Where `R` is the number of data repetitions and `f(R)` captures diminishing returns

## Key Findings
1. **4 epochs is the practical ceiling** — beyond this, extra repetitions barely help
2. **Compute can substitute for data** — if you can't get more data, train a bigger model
3. **Deduplication matters** — removing duplicates is more valuable than having more data
4. **Code mixing helps everything** — even general language tasks benefit from code data
5. **Filtering > quantity** — aggressive quality filtering beats having more diverse but noisy data

## Connections
- **Key concepts**: [[concepts/scaling-laws]], [[concepts/pre-training]]
- **Influenced**: [[sources/smollm2]] (overtraining strategy), [[sources/refinedweb]] (data quality focus)
- **Organizations**: [[entities/orgs/huggingface]]

## Citation
> Muennighoff et al., "Scaling Data-Constrained Language Models," arXiv:2305.16264, 2023.
> https://huggingface.co/papers/2305.16264
