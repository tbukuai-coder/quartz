---
type: source
arxiv_id: "2503.19786"
title: "Gemma 3 Technical Report"
authors: ["Google DeepMind"]
date: 2025-03-25
org: "Google"
tags: [multimodal, open-model, long-context, 2025]
upvotes: 55
---

# Gemma 3

> Google's third-generation open model family (1B–27B) with native vision understanding, 128K context via sliding-window local attention, and broader language coverage — achieving strong performance at practical sizes.

## Key Contributions
- Added **native vision capabilities** to the Gemma family for the first time (image + text input)
- Extended context to **128K tokens** using sliding-window local/global attention pattern with efficient KV-cache memory
- Broadened **language support** beyond English
- Models at **1B, 4B, 12B, and 27B** sizes — covering edge to server deployment
- **Post-training enhancements** including improved instruction following and safety

## Method
Architecture builds on Gemma 2's interleaved local-global attention but adds:
1. **Vision encoder**: SigLIP-based vision transformer for image understanding
2. **Interleaved local/global attention**: Alternating sliding-window (local) and full (global) attention layers — reduces KV-cache memory for long sequences
3. **128K context**: Achieved via the local attention pattern without requiring exotic positional encoding tricks
4. **Distillation**: Smaller models benefit from knowledge distillation from larger Gemma/Gemini models

## Results
- **Gemma 3 27B**: Competitive with Qwen2.5-32B and Llama 3.3-70B on many benchmarks at half the size
- **Vision tasks**: Strong image understanding comparable to dedicated VLMs
- **Long-context**: Reliable performance up to 128K tokens
- **Multilingual**: Improved performance across languages

## Models Released
- Gemma 3 1B, 4B, 12B, 27B (Base + IT variants, open weights)

## Connections
- **Builds on**: [[sources/gemma-2|Gemma 2]], [[sources/gemma|Gemma]]
- **Part of**: [[entities/models/gemma|Gemma]] family, [[entities/orgs/google|Google]]
- **Vision**: Uses [[sources/siglip|SigLIP]] vision encoder
- **Safety**: [[sources/shieldgemma|ShieldGemma]] built on Gemma 2 architecture
- **Related concepts**: [[concepts/vision-language-models|VLMs]], [[concepts/long-context|Long Context]], [[concepts/distillation|Distillation]]

## Citation
> Google DeepMind, "Gemma 3 Technical Report," arXiv:2503.19786, 2025.
