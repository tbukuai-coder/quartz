---
type: source
arxiv_id: "2406.16860"
title: "Cambrian-1: A Fully Open, Vision-Centric Exploration of Multimodal LLMs"
authors: ["Shengbang Tong", "Ellis Brown", "Penghao Wu", "Various"]
date: 2025-06-24
org: "NYU / Various"
tags: [vlm, multimodal, vision, open-science, 2025]
upvotes: 63
---

# Cambrian-1

> A vision-centric MLLM family that systematically explores visual representation learning for multimodal LLMs, introducing the Spatial Vision Aggregator (SVA) and CV-Bench. 1,995 GitHub ⭐.

## Key Contributions
- **Vision-centric approach**: Uses LLMs as an interface to rigorously evaluate and compare visual representations — filling a gap where vision components are often under-explored
- **Spatial Vision Aggregator (SVA)**: Novel connector that aggregates multi-scale visual features with spatial awareness, outperforming simpler projection layers
- **CV-Bench**: New benchmark specifically designed to evaluate visual grounding in MLLMs (beyond text-centric benchmarks)
- **Comprehensive ablation**: Evaluates 20+ vision encoder combinations, training strategies, and connector designs
- Fully open: weights, data, code (1,995 GitHub ⭐)

## Method
1. Evaluate diverse **vision encoders** (CLIP, SigLIP, DINOv2, SAM, etc.) as MLLM backends
2. Design **SVA**: aggregates features from multiple vision encoders while preserving spatial information
3. Introduce **CV-Bench**: tasks requiring spatial understanding (counting, positioning, relationships)
4. Train Cambrian-1 models (8B, 13B, 34B) with the best vision configurations

Key insight: Most MLLMs barely explore the vision side. Cambrian shows that vision encoder choice and connector design matter enormously.

## Results
- SVA outperforms linear/MLP connectors across MLLM benchmarks
- Best results with ensemble of complementary vision encoders (CLIP + DINOv2)
- CV-Bench reveals spatial grounding failures invisible in text-centric benchmarks
- Competitive with or better than LLaVA-NeXT, InternVL at matched scales

## Connections
- **Builds on**: [[sources/llava|LLaVA]], [[sources/clip|CLIP]], [[sources/siglip|SigLIP]], [[sources/sam|SAM]]
- **Related**: [[sources/idefics2|Idefics2]] (also ablates VLM design), [[sources/internvl-1-5|InternVL 1.5]]
- **Concepts**: [[concepts/vision-language-models|VLMs]], [[concepts/multimodal-models|Multimodal]]
- **Comparison**: [[comparisons/vision-language-models|VLM Comparison]]

## Citation
> Tong et al., "Cambrian-1: A Fully Open, Vision-Centric Exploration of Multimodal LLMs," arXiv:2406.16860, 2025.
