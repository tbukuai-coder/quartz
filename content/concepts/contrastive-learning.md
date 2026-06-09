---
type: concept
tags: [training, embeddings, pre-training, representation-learning]
---

# Contrastive Learning

> A training paradigm that learns representations by **pulling similar examples together and pushing dissimilar examples apart** in embedding space — the foundation of modern text embeddings, vision encoders, and multimodal alignment.

## Overview
Contrastive learning teaches models to create useful representations without explicit labels. By training a model to distinguish positive pairs (similar items) from negative pairs (dissimilar items), the model learns a structured embedding space where semantic similarity is captured by vector distance. This paradigm powers text embeddings ([[concepts/embeddings|SBERT, E5, Nomic Embed]]), vision encoders (CLIP, [[sources/siglip|SigLIP]]), and multimodal alignment.

## How It Works

### InfoNCE Loss
The standard contrastive objective:
```
L = -log(exp(sim(q, k⁺)/τ) / Σ_i exp(sim(q, k_i)/τ))
```

### Positive Pair Construction
| Domain | Positive Pairs | Source |
|---|---|---|
| **Text embeddings** | (query, relevant passage) | Web search logs, title-body pairs |
| **Vision (self-supervised)** | (augmented_view_1, augmented_view_2) | Same image, different crops |
| **Vision-language** | (image, caption) | Image-text datasets (LAION, CC) |
| **Sentence embeddings** | (sentence, paraphrase) | NLI datasets, parallel translations |

## Applications in the LLM Ecosystem

### Text Embeddings
[[sources/sentence-bert|SBERT]] → [[sources/e5|E5]] → [[sources/nomic-embed|Nomic Embed]]: All use contrastive learning as the core training paradigm.

### Vision Encoders for VLMs
- **CLIP**: Contrastive image-text pre-training (used by [[sources/llava|LLaVA]])
- **[[sources/siglip|SigLIP]]**: Sigmoid loss variant — scales better
- **InternViT**: Continuously trained for [[sources/internvl-1-5|InternVL]]

### Data Curation
Contrastive models enable data quality filtering: [[sources/fineweb|FineWeb-Edu]] uses classifier trained on contrastive embeddings to score educational quality.

## Key Variants
| Method | Key Innovation | Domain |
|---|---|---|
| **CLIP** | Image-text pairs, dual encoder | Multimodal |
| **[[sources/siglip|SigLIP]]** | Sigmoid loss (no global softmax) | Multimodal |
| **[[sources/sentence-bert|SBERT]]** | Siamese networks for sentence pairs | Text |
| **[[sources/e5|E5]]** | Weakly-supervised web pairs at scale | Text |

## Key Papers
- [[sources/sentence-bert]] — Siamese contrastive learning for sentence embeddings
- [[sources/e5]] — Weakly-supervised contrastive pre-training at scale
- [[sources/nomic-embed]] — Fully open contrastive embedding model
- [[sources/siglip]] — Sigmoid contrastive loss for vision-language

## See Also
- [[concepts/embeddings]] — Text embeddings (built on contrastive learning)
- [[concepts/vision-language-models]] — VLMs use contrastive-trained vision encoders
- [[concepts/distillation]] — Related paradigm for knowledge transfer