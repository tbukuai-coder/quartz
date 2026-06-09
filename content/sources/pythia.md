---
type: source
arxiv_id: "2304.01373"
title: "Pythia: A Suite for Analyzing Large Language Models Across Training and Scaling"
authors: ["Stella Biderman", "Hailey Schoelkopf", "Quentin Anthony", "et al."]
date: 2023-04-03
org: "EleutherAI"
tags: [scaling, interpretability, open-science, foundational, 2023]
upvotes: 9
---

# Pythia

> A suite of **16 LLMs** (70M–12B) trained on the **same data** (The Pile) under **identical conditions** — designed specifically for studying training dynamics, scaling, and interpretability. All 154 intermediate checkpoints released. The most comprehensive controlled scaling study in open LLM research.

## Key Contributions
- **Controlled scaling suite**: 16 models (70M to 12B) with identical data ordering, hyperparameters (scaled), and training setup
- **154 checkpoints per model**: Every ~2.1B tokens, enabling fine-grained study of training dynamics
- **Identical data**: All models see the same data in the same order (The Pile, 300B tokens, deduplicated)
- **Public and reproducible**: All code, data, checkpoints, and logs released
- **Research-enabling**: Specifically designed for the research community, not as production models

## Models
| Model | Params | Layers | Hidden | Heads |
|---|---|---|---|---|
| Pythia-70M | 70M | 6 | 512 | 8 |
| Pythia-160M | 160M | 12 | 768 | 12 |
| Pythia-410M | 410M | 24 | 1024 | 16 |
| Pythia-1B | 1B | 16 | 2048 | 8 |
| Pythia-1.4B | 1.4B | 24 | 2048 | 16 |
| Pythia-2.8B | 2.8B | 32 | 2560 | 32 |
| Pythia-6.9B | 6.9B | 32 | 4096 | 32 |
| Pythia-12B | 12B | 36 | 5120 | 40 |

All follow GPT-NeoX architecture. Trained on The Pile (deduplicated, 300B tokens, single epoch).

## Research Findings
The paper demonstrates several analyses enabled by the suite:

1. **Memorization**: Models memorize more as they get larger; memorization of specific sequences can be traced across checkpoints
2. **Few-shot learning**: Emerges at different scales for different tasks; strongly correlated with training loss
3. **Gender bias**: Bias patterns change during training and across scales — not monotonically related to model size
4. **Term frequency effects**: Model performance on specific tokens correlates with their frequency in training data

## Impact
Pythia has been cited extensively for:
- **Mechanistic interpretability**: Checkpoint availability enables studying how capabilities emerge
- **Data influence**: Studying how specific training data affects model behavior
- **Scaling laws**: Controlled comparisons across 3 orders of magnitude
- **Open-science template**: Influenced OLMo's fully-open release philosophy

## Connections
- Org: [[entities/orgs/eleutherai|EleutherAI]]
- Related: [[sources/olmo|OLMo]] (inspired by Pythia's open approach), [[sources/chinchilla|Chinchilla]] (scaling laws)
- Concepts: [[concepts/scaling-laws]], [[concepts/pre-training]]
- Data: The Pile (EleutherAI's pretraining corpus)

## Citation
> Biderman et al., "Pythia: A Suite for Analyzing Large Language Models Across Training and Scaling," ICML 2023, arXiv:2304.01373.
