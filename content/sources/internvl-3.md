---
type: source
arxiv_id: "2504.10479"
title: "InternVL3: Exploring Advanced Training and Test-Time Recipes for Open-Source Multimodal Models"
authors: ["Jinguo Zhu", "Weiyun Wang", "Zhe Chen", "et al."]
date: 2025-04-14
org: "Shanghai AI Lab / Tsinghua / CUHK"
tags: [multimodal, vlm, open-models, 2025]
upvotes: 308
---

# InternVL3

> The latest in the InternVL series — introducing **native multimodal pre-training** that jointly learns language and vision from scratch, achieving **72.2 on MMMU** (new open-source SOTA) and matching proprietary models like GPT-4o, Claude 3.5 Sonnet, and Gemini 2.5 Pro. **308 upvotes** on HF Papers — among the most upvoted papers ever.

## Key Contributions
- **Native multimodal pre-training**: Jointly acquires linguistic and multimodal capabilities in a single pre-training stage (vs. adapting a text-only LLM)
- **Variable Visual Position Encoding (V2PE)**: Supports extended multimodal contexts with variable-resolution images
- **Mixed Preference Optimization (MPO)**: Advanced post-training combining SFT with preference learning
- **Test-Time Scaling**: Best-of-N evaluation with VisualPRM-8B as critic model
- **Full size range**: 1B, 2B, 8B, 14B, 38B, and 78B parameter models
- **72.2 MMMU**: New open-source SOTA, competitive with GPT-4o

## Method
### Architecture: ViT-MLP-LLM
- **Vision encoder**: InternViT (300M–6B)
- **Connector**: 2-layer MLP projecting vision tokens to LLM input space
- **LLM backbone**: InternLM2.5 or Qwen2.5 series
- **Dynamic resolution**: Variable number of visual tokens based on image complexity

### Native Multimodal Pre-Training
Unlike conventional approaches (pretrain text-only LLM → add vision adapter):
1. **Single stage**: Language and vision training happen simultaneously
2. **Interleaved data**: Mix of pure text, image-text, and multi-image data during pretraining
3. **Better alignment**: Avoids the alignment gap from adapting a frozen text model to vision
4. **Result**: InternVL3-8B with native pretraining outperforms conventional InternVL2-8B pipeline

### Post-Training
1. **SFT**: Diverse multimodal instruction data (knowledge, math, OCR, video, grounding)
2. **MPO (Mixed Preference Optimization)**: Combines DPO-style preference learning with supervised signal
3. **Test-Time Scaling**: VisualPRM-8B scores multiple generated answers; best one selected

## Results
| Model | MMMU | MathVista | DocVQA | OCRBench | Video-MME | Overall |
|---|---|---|---|---|---|---|
| **InternVL3-78B** | **72.2** | **72.9** | **95.1** | **904** | **72.2** | **SOTA open** |
| GPT-4o | 69.1 | 63.8 | 92.8 | 736 | 71.9 | Below InternVL3 |
| Claude 3.5 Sonnet | 68.3 | 67.7 | 95.2 | 788 | — | Competitive |
| Gemini 2.5 Pro | — | — | 93.9 | — | — | Competitive |
| InternVL2.5-78B | 70.1 | 67.4 | 94.2 | 877 | 72.1 | Previous SOTA |

### Scaling Efficiency
| Model | Params | MMMU | Notable |
|---|---|---|---|
| InternVL3-1B | 1B | 43.4 | Best at this scale |
| InternVL3-8B | 8B | 62.0 | Beats many 70B+ models |
| InternVL3-38B | 38B | 69.7 | Matches GPT-4o |
| InternVL3-78B | 78B | 72.2 | New open SOTA |

## Capabilities
- **OCR & Document**: 95.1 DocVQA, 904 OCRBench — SOTA on document understanding
- **Math**: 72.9 MathVista — strong multimodal math reasoning
- **Video**: 72.2 Video-MME — competitive video understanding
- **GUI Grounding**: 88.7 ScreenSpot — strong for agent applications
- **Multilingual**: Evaluated on MTVQA, MMMB with strong non-English performance
- **Language preservation**: Maintains strong pure-text performance (86.9 MMLU for 78B)

## Connections
- Builds on: [[sources/internvl-1-5|InternVL 1.5]], [[sources/internvl-2-5|InternVL 2.5]]
- Models: [[entities/models/internvl|InternVL family]]
- Org: [[entities/orgs/shanghai-ai-lab|Shanghai AI Lab]]
- Concepts: [[concepts/vision-language-models|VLMs]], [[concepts/multimodal-models|Multimodal]]
- Comparisons: [[comparisons/vision-language-models]]

## Citation
> Zhu et al., "InternVL3: Exploring Advanced Training and Test-Time Recipes for Open-Source Multimodal Models," arXiv:2504.10479, 2025.
