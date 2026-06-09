---
type: entity
category: model
tags: [open-models, alibaba, multilingual, reasoning, moe, multimodal]
---

# Qwen (Qwen2.5 → Qwen3)

> Alibaba's comprehensive LLM series — notable for the **widest size range** (0.6B–235B), **multilingual strength** (119 languages in Qwen3), state-of-the-art reasoning with unified thinking/non-thinking modes, and a leading vision-language extension (Qwen2.5-VL). The most upvoted model paper on HF Papers (339 upvotes).

## Overview
The Qwen series from Alibaba's Qwen team has rapidly evolved from Qwen1 to Qwen3, with each iteration dramatically improving data scale, model quality, and capabilities. Qwen3 introduces a groundbreaking **unified thinking mode** — a single model that can switch between fast responses and deep reasoning — eliminating the need for separate chat and reasoning deployments. The **Qwen2.5-VL** series extends these capabilities to vision and video understanding. **Qwen2-Audio** and **Qwen2.5-Omni** extend to audio and omni-modal capabilities.

## Models

### Qwen3 (2025)
| Model | Params | Active | Architecture | Context |
|---|---|---|---|---|
| Qwen3-0.6B | 0.6B | 0.6B | Dense | 32K |
| Qwen3-1.7B | 1.7B | 1.7B | Dense | 32K |
| Qwen3-4B | 4B | 4B | Dense | 32K |
| Qwen3-8B | 8B | 8B | Dense | 32K |
| Qwen3-14B | 14B | 14B | Dense | 32K |
| Qwen3-32B | 32B | 32B | Dense | 32K |
| Qwen3-30B-A3B | 30B | 3B | MoE (128 experts) | 32K |
| Qwen3-235B-A22B | 235B | 22B | MoE (128 experts) | 32K |

### Qwen2.5-VL (2025) — Vision-Language
| Model | Params | Key Capability |
|---|---|---|
| Qwen2.5-VL-3B | ~3B | Edge/mobile multimodal |
| Qwen2.5-VL-7B | ~7B | Balanced VLM |
| Qwen2.5-VL-72B | ~72B | GPT-4o competitive, visual agent |

### Qwen2.5-Omni (2025) — Omni-Modal
| Model | Params | Key Capability |
|---|---|---|
| Qwen2.5-Omni-7B | ~7B | Text + image + audio + video → text + speech |

### Qwen2-Audio (2024) — Audio-Language
| Model | Params | Key Capability |
|---|---|---|
| Qwen2-Audio-7B | ~7B | Audio understanding + voice chat |
| Qwen2-Audio-Instruct | ~7B | Instruction-following audio analysis |

### Qwen2.5 (2024)
| Model | Year | Params | Training Data | Key Features |
|---|---|---|---|---|
| Qwen2.5 | 2024 | 0.5B–72B | 18T tokens | Comprehensive size range, 128K context |
| Qwen2.5-Coder | 2024 | 1.5B–32B | 5.5T tokens | Code-specialized |
| Qwen2.5-Math | 2024 | 1.5B–72B | — | Math reasoning specialized |
| Qwen2.5-1M | 2025 | 7B, 14B | — | 1M token context |

## Key Innovations (Qwen3)
- **Unified thinking modes**: `/think` for step-by-step reasoning, `/no_think` for fast responses — in a single model
- **Thinking budget mechanism**: Control how many tokens the model spends "thinking" per query
- **MoE scaling**: 235B total params with only 22B active — efficiency + capability
- **119 languages** (up from 29 in Qwen2.5)
- **4-stage post-training**: Long-CoT cold start → Reasoning RL → Thinking mode fusion → General RL

## Key Innovations (Qwen2.5-VL)
- **Native dynamic-resolution ViT**: Trained from scratch with Window Attention
- **Multimodal RoPE (M-RoPE)**: Encodes temporal + spatial positions jointly
- **Hours-long video understanding** with second-level event localization
- **Visual agent**: Can operate computers and mobile devices

## Key Innovations (Qwen2.5-Omni)
- **TMRoPE**: Time-aligned Multimodal RoPE for audio-video synchronization
- **Thinker-Talker architecture**: Separate text generation (Thinker) and speech generation (Talker) to avoid modality interference
- **Streaming speech output**: Sliding-window DiT for low-latency streaming
- Speech input achieves **text-parity** on reasoning benchmarks (MMLU, GSM8K)

## Architecture
- Transformer decoder with GQA, QKV bias
- RoPE embeddings, SwiGLU, RMSNorm
- MoE variants with 128 experts, grouped routing (8 groups)
- Up to 128K+ context (via YaRN extension)

## Ecosystem Role
Qwen models are widely used as base models for:
- [[sources/deepseek-r1]] distillation (Qwen2.5-1.5B through 32B)
- [[sources/s1|s1 reasoning]] (SFT on Qwen2.5-32B-Instruct)
- [[sources/open-reasoner-zero|Open-Reasoner-Zero]] (RL on Qwen2.5-32B base)
- Community fine-tuning for various tasks
- Reasoning model development (Qwen3 is the premier open reasoning model)

## Related Papers
- [[sources/qwen3]] — Qwen3 Technical Report
- [[sources/qwen25]] — Qwen2.5 Technical Report
- [[sources/qwen25-vl]] — Qwen2.5-VL Technical Report
- [[sources/qwen2-vl]] — Qwen2-VL Technical Report
- [[sources/qwen2-audio]] — Qwen2-Audio Technical Report
- [[sources/qwen25-omni]] — Qwen2.5-Omni Technical Report
- [[sources/qwen25-coder]] — Qwen2.5-Coder Technical Report

## See Also
- [[entities/orgs/alibaba]]
- [[concepts/grpo]]
- [[concepts/mixture-of-experts]]
- [[concepts/vision-language-models]]
- [[concepts/multimodal-models]]
- [[concepts/scaling-laws]]
