---
type: source
arxiv_id: "2401.02954"
title: "Mixtral of Experts"
authors: ["Mistral AI"]
date: 2024-01-08
org: "Mistral AI"
tags: [open-models, moe, architecture, 2024]
upvotes: 160
---

# Mistral Small / Mistral Large / Codestral

> Beyond Mixtral, Mistral AI released a family of dense and MoE models spanning from **Mistral Small** (24B) to **Mistral Large** (123B) and specialized models like **Codestral** (code) and **Pixtral** (vision). This page covers the broader Mistral ecosystem beyond the [[sources/mistral-7b]] and [[sources/mixtral]] papers.

**Note**: The core Mixtral 8x7B paper already exists at [[sources/mixtral]]. This entry documents the broader Mistral model family released without formal papers.

## The Mistral Ecosystem (2024–2025)

| Model | Year | Params | Type | Key Feature |
|---|---|---|---|---|
| Mistral 7B | 2023 | 7B | Dense | GQA + SWA, Apache 2.0 |
| Mixtral 8x7B | 2024 | 47B (13B active) | MoE | First open-source MoE |
| Mixtral 8x22B | 2024 | 176B (44B active) | MoE | Larger MoE |
| Mistral Small | 2024 | 24B | Dense | Efficient reasoning |
| Mistral Large | 2024 | 123B | Dense | Frontier dense model |
| Codestral | 2024 | 22B | Dense | Code-specialized |
| Pixtral | 2024 | 12B | Multimodal | Vision-language model |
| Mistral Nemo | 2024 | 12B | Dense | Joint with NVIDIA |

## Key Characteristics
- **No formal papers**: Mistral AI typically releases models with minimal documentation (blog posts, model cards)
- **Fast iteration**: New models every few months
- **Strong efficiency**: Consistently outperform larger models
- **Permissive licensing**: Mix of Apache 2.0 and custom licenses
- **French AI**: First European lab competitive with US/Chinese labs

## See Also
- [[sources/mistral-7b]] — Mistral 7B paper
- [[sources/mixtral]] — Mixtral 8x7B paper
- [[entities/models/mistral]] — Mistral model entity
- [[entities/orgs/mistral-ai]] — Mistral AI org
