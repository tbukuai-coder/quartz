---
type: source
arxiv_id: "2408.06072"
title: "CogVideoX: Text-to-Video Diffusion Models with An Expert Transformer"
authors: ["Zhuoyi Yang", "Jiayan Teng", "Wendi Zheng", "Ming Ding", "Shiyu Huang", "Jiazheng Xu", "Yuanming Yang", "Wenyi Hong", "Xiaohan Zhang", "Guanyu Feng"]
date: 2024-08-12
org: "Tsinghua / Zhipu AI"
tags: [video-generation, diffusion, multimodal, 2024]
upvotes: 38
---

# CogVideoX

> An open-source text-to-video diffusion model using a 3D VAE for spatiotemporal compression and an expert transformer for deep text-video fusion — the most HF-ecosystem-integrated open video generation model. 12K+ GitHub stars.

## Key Contributions
- **3D Variational Autoencoder**: Compresses video along both spatial and temporal dimensions (4×8×8 compression ratio) — much more efficient than frame-by-frame encoding
- **Expert transformer with adaptive LayerNorm**: Separate expert parameters for text and video modalities via adaptive layer normalization — deeper fusion than cross-attention
- **Progressive training**: Start with low resolution/short duration, progressively increase — stabilizes training and improves quality
- **Fully open**: Weights on HF Hub, training code, inference pipeline in diffusers

## Method
1. **3D VAE**: Encodes video V ∈ R^(T×H×W×3) into latent z ∈ R^(T/4×H/8×W/8×C). Uses 3D causal convolutions that process space and time jointly — captures temporal coherence that 2D VAEs miss
2. **Expert Transformer**: Full-attention transformer operating on concatenated text+video tokens. Uses expert adaptive LayerNorm: different scale/shift parameters for text vs. video tokens, enabling modality-specific processing within shared attention
3. **Progressive training**: 3 stages:
   - Stage 1: Low-res (256px), short clips (2s)
   - Stage 2: Medium-res (480px), medium clips (4s)
   - Stage 3: High-res (720px), longer clips (6s)
4. **Video captioning**: Trained a video captioner to generate detailed descriptions for training data — quality of captions drives quality of generation

## Results
- Generates coherent 6-second videos at 720p from text prompts
- Strong temporal consistency — objects maintain identity across frames
- Text-video alignment on par with or exceeding Pika, Gen-2 (closed models)
- Models on HF Hub: CogVideoX-2B, CogVideoX-5B (with I2V and T2V variants)
- Integrated into HuggingFace `diffusers` library

## Models Released
- **CogVideoX-2B** — text-to-video (T2V)
- **CogVideoX-5B** — T2V and image-to-video (I2V)
- Available at `THUDM/CogVideoX-5b` on HF Hub

## Connections
- Extends: [[sources/latent-diffusion|Latent Diffusion / Stable Diffusion]] (from images to video)
- Related: [[concepts/diffusion-models|Diffusion Models]]
- Tools: HuggingFace `diffusers` library integration
- Org: Tsinghua / Zhipu AI (THUDM)

## Citation
> Yang et al., "CogVideoX: Text-to-Video Diffusion Models with An Expert Transformer," arXiv:2408.06072, 2024.
