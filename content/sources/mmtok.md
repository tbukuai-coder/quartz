---
type: source
arxiv_id: "2508.18264"
title: "MMTok: Multimodal Coverage Maximization for Efficient Inference of VLMs"
authors: ["Sixun Dong", "Juhua Hu", "Mian Zhang", "Ming Yin", "Yanjie Fu", "Qi Qian"]
date: 2025-08-27
org: "UCF / Amazon / Various"
tags: [vlm, inference-efficiency, token-pruning, multimodal, training-free, 2025]
upvotes: 25
---

# MMTok: Multimodal Token Optimization for VLM Inference

> A **training-free** vision token selection method that formulates token pruning as a **Maximum Coverage** problem — jointly optimizing text-vision and vision-vision coverage via greedy submodular optimization. Achieves **1.87× speedup** on LLaVA-NeXT-13B at 98.7% performance, and retains 87.7% performance with only **4 vision tokens** on LLaVA-1.5-7B.

## Key Contributions
- **Multimodal criterion**: Identifies the key failure of prior token pruning methods — using **unimodal** criteria (vision-only attention or text-only relevance) ignores the inherently bimodal nature of VLM tasks
- **Maximum Coverage formulation**: Vision token selection as a submodular optimization problem with (1-1/e)-approximation guarantee via greedy algorithm
- **Dual coverage**: Text-Vision coverage (select tokens covering text query semantics) + Vision-Vision coverage (select tokens covering full visual content diversity) — jointly optimized
- **Training-free**: Plugs into any VLM at inference time with no fine-tuning or additional training
- **Optional agentic extension**: MMTok_Agent uses a lightweight VLM (SmolVLM2-256M) to generate preliminary answers, enriching text tokens for better query-guided pruning
- **Extreme compression**: Retains 87.7% performance with only **4 vision tokens** (99.3% token reduction)

## Method
Given n vision tokens {v_1,...,v_n} and text query tokens {t_1,...,t_m}:
1. **Text-Vision coverage**: Maximize similarity between selected vision tokens and text tokens — finds query-relevant visual regions
2. **Vision-Vision coverage**: Maximize similarity between selected tokens and all vision tokens — ensures visual completeness
3. **Greedy submodular optimization**: Both problems solved via greedy algorithm (polynomial time, near-optimal)
4. **Balancing**: α=0.5 between T-V and V-V objectives; row-wise softmax with temperatures τ_t=0.02, τ_v=0.2

Key insight: Vision and text information are **complementary** for token selection — unimodal approaches discard half the useful signal.

## Results
### LLaVA-1.5-7B (576 → 64 tokens, 89% reduction)
| Method | Retained Performance |
|---|---|
| FastV | 75.6% |
| SparseVLM | 86.9% |
| VisionZip (no FT) | 93.2% |
| DivPrune | 94.8% |
| **MMTok** | **96.5%** |

### LLaVA-NeXT-13B
- At 160/2880 tokens (5.5% retained): >95% performance, **1.87× speedup** on POPE
- At 192 tokens: **98.7% performance** vs DivPrune 98.0%, VisionZip 97.9%

### Extreme Compression (LLaVA-1.5-7B, 4 tokens)
- **87.7% retained** — useful for extreme edge-deployment scenarios

### Generalization
- Consistent SOTA across LLaVA-1.5-7B/13B, LLaVA-NeXT-7B/13B, and Qwen-2.5-VL-7B

## Connections
- **Builds on**: [[sources/llava|LLaVA]], [[sources/clip|CLIP]] (vision encoders)
- **Related**: VisionZip, FastV, SparseVLM, DivPrune (prior token pruning methods)
- **Concepts**: [[concepts/vision-language-models|VLMs]], [[concepts/llm-serving|LLM Serving]]
- **Comparison**: [[comparisons/vision-language-models|VLM Comparison]]
- **GitHub**: https://github.com/Ironieser/MMTok

## Citation
> Dong et al., "MMTok: Multimodal Coverage Maximization for Efficient Inference of VLMs," arXiv:2508.18264, 2025.
