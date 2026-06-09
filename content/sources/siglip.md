---
type: source
arxiv_id: "2303.15343"
title: "Sigmoid Loss for Language Image Pre-Training"
authors: ["Xiaohua Zhai", "Basil Mustafa", "Alexander Kolesnikov", "Lucas Beyer"]
date: 2023-03-27
org: "Google Brain"
tags: [vision, contrastive-learning, image-text, foundational, 2023]
upvotes: 11
---

# SigLIP — Sigmoid Loss for Vision-Language Pre-Training

> Replaces CLIP's softmax contrastive loss with a simpler pairwise sigmoid loss — enabling better small-batch training and becoming the default vision encoder for modern VLMs (InternVL, SmolVLM, Gemma 3). 2M+ HF downloads.

## Key Contributions
- **Pairwise sigmoid loss**: Each image-text pair is scored independently — no global batch normalization needed (unlike CLIP's softmax cross-entropy)
- **Batch-size friendly**: Works well at both small (4K) and large (32K+) batch sizes — CLIP degrades at small batches
- **Compute-efficient**: Train ViT-B/16 on just 4 TPUv4 chips to match CLIP performance
- **Foundation for modern VLMs**: SigLIP encoders used in [[sources/smolvlm|SmolVLM]], [[sources/idefics2|Idefics2]], [[sources/internvl-1-5|InternVL 1.5]], Gemma 3, PaLI-3

## Method
1. **CLIP loss (softmax)**: Normalize similarities across the batch → requires seeing all pairs → doesn't decompose across devices
2. **SigLIP loss (sigmoid)**: For each (image, text) pair, apply sigmoid: `L = -log σ(z_ij · t)` where z_ij = 1 for matching pairs, -1 for non-matching. Each pair scored independently
3. **Advantages**: No communication needed for normalization → simpler distributed training. Loss decomposes per-pair → batch size becomes a true hyperparameter, not a constraint
4. **Training**: Standard ViT architectures (B/16, L/16, SO400M) trained on WebLI dataset

## Results
- SigLIP-B/16: 84.5% ImageNet zero-shot (vs. CLIP-B/16: ~68%)
- SigLIP-SO400M: Best open vision encoder for VLM applications
- Better than CLIP at small batch sizes (4K–8K)
- Matches CLIP at large batch sizes (32K)
- Lower compute requirements for same performance

## Models Released
- **SigLIP-SO400M-patch14-384** — 2M+ HF downloads, default VLM vision encoder
- SigLIP-B/16, L/16 variants
- SigLIP 2 (2024) — updated version

## Connections
- Replaces: CLIP (OpenAI) as preferred vision encoder
- Used by: [[sources/smolvlm|SmolVLM]], [[sources/idefics2|Idefics2]], [[sources/internvl-1-5|InternVL]], Gemma 3
- Related: [[concepts/vision-language-models|Vision-Language Models]], [[concepts/multimodal-models|Multimodal Models]]
- Org: [[entities/orgs/google|Google]]

## Citation
> Zhai et al., "Sigmoid Loss for Language Image Pre-Training," ICCV 2023, arXiv:2303.15343.
