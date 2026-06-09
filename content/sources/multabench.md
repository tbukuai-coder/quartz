---
type: source
arxiv_id: "2605.10616"
title: "MulTaBench: Benchmarking Multimodal Tabular Learning with Text and Image"
authors: ["Alan Arazi", "Eilam Shapira", "Shoham Grunblat", "Mor Ventura", "Elad Hoffer", "Gioia Blayer", "David Holzmüller", "Lennart Purucker", "Gaël Varoquaux", "Frank Hutter"]
date: 2026-05-14
org: "Multi-institution"
tags: [benchmark, tabular, multimodal, embeddings, 2026]
upvotes: 140
---

# MulTaBench: Benchmarking Multimodal Tabular Learning with Text and Image

> First comprehensive benchmark for multimodal tabular learning revealing that task-specific embedding tuning outperforms frozen pretrained embeddings, and that predictive gains from multimodal features depend on complementary signal across modalities.

## Key Contributions
- **MulTaBench benchmark**: systematic evaluation framework for tabular models that integrate text and image features alongside structured data
- **Task-specific tuning insight**: tuning embeddings to the target task consistently outperforms using frozen pretrained embeddings
- **Complementary signal analysis**: multimodal gains are largest when text/image features provide genuinely complementary predictive information (not redundant with tabular features)
- **Joint modeling advantage**: demonstrates benefits of end-to-end joint modeling over late fusion of frozen features
- Establishes best practices for multimodal tabular foundation models

## Method
MulTaBench evaluates tabular foundation models on datasets containing structured (numerical/categorical) data alongside unstructured (text, image) features. The benchmark tests: (1) frozen pretrained embeddings vs task-specific tuning; (2) modality contributions (when do text/image features help?); (3) joint vs separate modeling approaches. Datasets are curated to systematically vary the complementarity between structured and unstructured features.

## Results
- Task-specific embedding tuning consistently improves over frozen features
- Gains are strongest when modalities provide complementary (non-redundant) predictive signals
- Joint modeling outperforms late fusion approaches
- Establishes baseline performance across diverse multimodal tabular tasks

## Connections
- Builds on: [[sources/tabembed]], [[concepts/embeddings]], [[concepts/contrastive-learning]]
- Related: [[concepts/fine-tuning]], [[concepts/multimodal-models]]
- Fills gap: systematic evaluation of multimodal tabular learning

## Citation
> Arazi et al., "MulTaBench: Benchmarking Multimodal Tabular Learning with Text and Image," arXiv:2605.10616, 2026.
