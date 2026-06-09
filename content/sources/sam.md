---
type: source
arxiv_id: "2304.02643"
title: "Segment Anything"
authors: ["Alexander Kirillov", "Eric Mintun", "Nikhila Ravi", "et al."]
date: 2023-04-05
org: "Meta AI"
tags: [vision, segmentation, foundation-model, 2023]
upvotes: 50
---

# SAM: Segment Anything Model

> The **foundation model for image segmentation** — trained on **1 billion masks** from **11 million images**, SAM can segment any object in any image given a point, box, or text prompt. Established the paradigm of **promptable vision foundation models** analogous to GPT-3's impact on NLP. 47K+ GitHub stars.

## Key Contributions
- **Promptable segmentation**: Segment any object via point clicks, bounding boxes, or text prompts
- **SA-1B dataset**: 1 billion masks on 11 million images — largest segmentation dataset ever
- **Zero-shot transfer**: Generalizes to unseen objects and domains without fine-tuning
- **Data engine**: Iterative model-in-the-loop annotation pipeline that scales data collection
- **Foundation model for vision**: Analogous to GPT-3/BERT for NLP — a general-purpose visual backbone

## Method
### Architecture
```
Image → Image Encoder (ViT-H, run once)
Prompt (point/box/text) → Prompt Encoder
    → Lightweight Mask Decoder → Predicted masks
```
- **Image encoder**: ViT-H (632M params), pre-trained with MAE, processes image once
- **Prompt encoder**: Encodes points, boxes, text, or masks as positional embeddings
- **Mask decoder**: Lightweight transformer (2 layers) — runs in milliseconds per prompt
- **Amortized inference**: Heavy image encoding done once; mask decoding is fast per prompt

### SA-1B Data Engine
Three stages:
1. **Assisted manual**: Human annotators use SAM to accelerate labeling
2. **Semi-automatic**: SAM predicts, humans verify and add missing masks
3. **Fully automatic**: SAM generates masks for all objects autonomously

## Results
- **Zero-shot**: Competitive with fully supervised models on 23 diverse segmentation datasets
- **Interactive**: Real-time segmentation at ~50ms per prompt (after image encoding)
- **SA-1B**: 400× more masks than any previous segmentation dataset

## Impact
- **47K+ GitHub stars** — one of the most popular AI projects ever
- **SAM 2** (2024): Extended to video segmentation
- **Medical SAM**: Widely adapted for medical image segmentation
- **Robotics**: Used for object detection and manipulation
- **HF Integration**: `facebook/sam-vit-huge` among most downloaded vision models
- Established the "foundation model" paradigm for computer vision (beyond classification)

## Connections
- Org: [[entities/orgs/meta|Meta AI]]
- Extended by: SAM 2 (video), MedSAM, EfficientSAM
- Related: [[sources/clip|CLIP]] (vision-language), [[concepts/contrastive-learning]]

## Citation
> Kirillov et al., "Segment Anything," ICCV 2023, arXiv:2304.02643.
