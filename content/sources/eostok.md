---
type: source
arxiv_id: "2605.00503"
title: "End-to-End Autoregressive Image Generation with 1D Semantic Tokenizer"
authors: ["Wenda Chu", "Bingliang Zhang", "Jiaqi Han", "Yizhuo Li", "Linjie Yang", "Yisong Yue", "Qiushan Guo"]
date: 2026-05-02
org: "Unknown"
tags: [image-generation, autoregressive-models, visual-tokenizers, end-to-end-training, vision, 2026]
upvotes: 2
---

# EOSTok: End-to-End Autoregressive Image Generation with 1D Semantic Tokenizer

> An end-to-end single-stage training paradigm (EOSTok) that jointly optimizes reconstruction, autoregressive generation, and semantic alignment — achieving SOTA FID 1.48 on ImageNet-1K 256×256 without guidance.

## Key Contributions

- **End-to-end joint optimization**: Trains tokenizer and generative model together with direct generative feedback to the tokenizer (vs. conventional separate two-stage training)
- **Autoregressive Prediction Reconstruction (APR) loss**: Decodes teacher-forcing AR predictions into pixel space and computes reconstruction loss, bridging the gap between discrete token prediction and final generative quality
- **Implicit VFM alignment**: Aligns hidden patch embeddings (not 1D latent sequence directly) to vision foundation model representations, avoiding raster-ordered degeneration
- **1D semantic tokenizer**: Removes 2D structural dependency, naturally supporting vanilla autoregressive modeling without aggressive compression trade-offs

## Method

Prior approaches fall into two categories:
1. **2D tokenizers with non-raster AR** (masked AR, multi-scale prediction) — retain spatial layout but require complex generation schemes
2. **1D tokenizers** (TiTok etc.) — achieve high compression but sacrifice reconstruction quality

EOSTok bridges both by:
- Using 1D tokenization without aggressive compression (learnable query tokens compress global visual info)
- Jointly optimizing reconstruction + generation + semantic alignment in a single stage
- Distilling VFM semantics into hidden patch embeddings rather than the 1D latent sequence

## Results

- **EOSTok-H (644M params)**: FID **1.48** on ImageNet-1K 256×256 without guidance — **SOTA**
- Outperforms prior 1D and 2D tokenizer approaches
- Easily scalable architecture

## Connections
- Builds on: [[sources/titok]], [[sources/llamagen]], [[sources/var]], [[concepts/tokenization]]
- Related concepts: [[concepts/diffusion-models]], [[concepts/vision-language-models]], [[concepts/multimodal-models]]
- Related papers: [[sources/sd3]], [[sources/dit]], [[sources/rectified-flow]]
- Cited by / Influenced: Autoregressive visual generation, tokenizer design

## Citation
> Chu et al., "End-to-End Autoregressive Image Generation with 1D Semantic Tokenizer," arXiv:2605.00503, 2026.
