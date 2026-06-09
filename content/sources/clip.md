---
type: source
arxiv_id: "2103.00020"
title: "Learning Transferable Visual Models From Natural Language Supervision"
authors: ["Alec Radford", "Jong Wook Kim", "Chris Hallacy", "et al."]
date: 2021-02-26
org: "OpenAI"
tags: [multimodal, contrastive-learning, vision, foundational]
upvotes: 20
---

# CLIP: Contrastive Language-Image Pre-training

> Trained a **vision-language model** on **400M image-text pairs** from the web using **contrastive learning** — achieving remarkable **zero-shot transfer** to downstream vision tasks without task-specific training. CLIP became the foundation for modern text-to-image generation (Stable Diffusion, DALL-E), VLMs, and open-vocabulary recognition.

## Key Contributions
- **Contrastive pre-training**: Learn aligned image-text representations by matching images to their captions and vice versa
- **Zero-shot transfer**: Classify images by computing similarity to text descriptions of classes — no task-specific training needed
- **Scale-driven**: 400M web-scraped image-text pairs (WIT dataset) — showed data scale matters more than architecture
- **Versatile backbone**: Image encoder (ViT or ResNet) usable for classification, retrieval, generation
- **Natural language supervision**: Text provides richer supervision than categorical labels

## Method
```
Image → Image Encoder (ViT-L/14) → image embedding
Text  → Text Encoder (Transformer) → text embedding
                                        ↓
        Contrastive loss: maximize similarity of matched pairs,
        minimize similarity of unmatched pairs (InfoNCE)
```

### Training
- **400M image-text pairs** scraped from the web (WebImageText / WIT)
- **Contrastive objective**: For a batch of N pairs, predict which of N×N pairings are correct
- **Dual encoder**: Separate image and text encoders, aligned via learned temperature-scaled cosine similarity
- **Efficient**: No cross-attention between modalities — enables fast retrieval

## Results
### Zero-Shot Classification
| Model | ImageNet (0-shot) | Training |
|---|---|---|
| **CLIP ViT-L/14** | **76.2%** | 400M pairs, no ImageNet training |
| ResNet-50 (supervised) | 76.1% | 1.3M ImageNet labels |
| CLIP ResNet-50 | 58.2% | 400M pairs |

CLIP ViT-L/14 matches a fully supervised ResNet-50 without seeing any ImageNet labels.

### Robustness
- CLIP shows much better distribution shift robustness than supervised models
- Performance degrades gracefully on corrupted/shifted data

## Impact
CLIP is arguably the most impactful vision paper of the 2020s:
- **Text-to-image**: CLIP text encoder is the conditioning backbone for [[sources/latent-diffusion|Stable Diffusion]], DALL-E 2, [[sources/sdxl|SDXL]], [[sources/sd3|SD3]]
- **VLMs**: CLIP ViT used as vision encoder in [[sources/llava|LLaVA]], [[sources/idefics2|Idefics2]]
- **[[sources/siglip|SigLIP]]**: Improved CLIP with sigmoid loss (used in Gemma VLMs)
- **Open-vocabulary detection**: CLIP enables recognizing any object described in text
- **Embeddings**: Foundation for image-text retrieval systems
- **400M+ downloads**: Most downloaded model family on Hugging Face Hub

## Connections
- Extended by: [[sources/siglip|SigLIP]], OpenCLIP, [[sources/nomic-embed|Nomic Embed]] (concepts)
- Used by: [[sources/latent-diffusion]], [[sources/sdxl]], [[sources/llava]], [[sources/idefics2]]
- Org: [[entities/orgs/openai|OpenAI]]
- Concepts: [[concepts/contrastive-learning]], [[concepts/multimodal-models]], [[concepts/embeddings]]

## Citation
> Radford et al., "Learning Transferable Visual Models From Natural Language Supervision," ICML 2021, arXiv:2103.00020.
