---
type: concept
tags: [video-generation, diffusion, multimodal, 2025]
---

# Video Generation

> AI-powered video synthesis from text, images, or other videos — evolved from early U-Net diffusion models to DiT-based systems capable of minute-scale coherent generation.

## Overview
Video generation has rapidly advanced from producing short, low-quality clips to creating minute-scale, high-quality videos with consistent subjects, coherent motion, and narrative structure. The field builds on image diffusion foundations but adds temporal modeling challenges: motion consistency, long-horizon coherence, and subject persistence.

## Evolution

| Era | Approach | Duration | Quality | Key Work |
|---|---|---|---|---|
| 2022–2023 | U-Net + temporal layers | 2–4 sec | Low-medium | [[sources/svd|SVD]], early AnimateDiff |
| 2024 | DiT-based diffusion | 5–15 sec | Medium-high | [[sources/cogvideox|CogVideoX]], Sora (proprietary) |
| 2025 | Full-stack DiT + RLHF + distillation | **60+ sec** | **High** | [[sources/seedance|Seedance 1.0]], [[sources/self-forcing-pp|Self-Forcing++]] |
| 2026 | Specialized tasks + active TTS optimization | Variable | **Task-specific SOTA** | [[sources/sparkle-video-bg-replacement|Sparkle]], [[sources/swifti2v-highres|SwiftI2V]], [[sources/stream-t1|Stream-T1]] |

## Key Techniques

### Architecture
- **Diffusion Transformers (DiT)**: Replaced U-Net as backbone — [[sources/dit|DiT]], [[sources/sd3|SD3]]
- **Rectified Flow**: Straight-line generation paths for fewer sampling steps — [[concepts/rectified-flow|Rectified Flow]]
- **Autoregressive + Diffusion hybrid**: Generate frames autoregressively with diffusion quality

### Temporal Modeling
- **Temporal attention layers**: Cross-frame attention for motion consistency
- **3D convolutions**: Spatiotemporal feature extraction
- **Position embeddings**: Temporal position encoding for frame ordering

### Long-Horizon Generation
- **Self-Forcing++ paradigm**: Use self-generated long videos as training data — [[sources/self-forcing-pp|Self-Forcing++]]
- **Multi-shot generation**: Consistent subjects across separate video segments
- **Progressive resolution/duration**: Train short→long, low-res→high-res

### Quality Optimization
- **Video-specific RLHF**: Reward models for temporal fluidity, structural stability, instruction adherence — [[sources/seedance|Seedance 1.0]]
- **Multi-stage distillation**: Compress inference cost while maintaining quality

## Active Test-Time Scaling: Stream-T1

[[sources/stream-t1|Stream-T1 (2026)]] pioneers **active test-time scaling for streaming video generation** — shifting from passive candidate selection to active optimization of the generation process itself:

### Why Streaming Video for TTS?
Current TTS methods (ImagerySearch) denoise entire videos simultaneously in a global high-dimensional space. Each candidate requires massive multi-step denoising, severely limiting search efficiency. Streaming generation operates chunk-by-chunk with few denoising steps (e.g., 4 per chunk), making it intrinsically aligned with TTS principles.

### Three Active Components
1. **Stream-Scaled Noise Propagation**: Refines initial latent noise via spherical interpolation with historically proven high-quality trajectories: $x_T^n = \beta x_T^{n-1} + \sqrt{1-\beta^2}\,\epsilon$
2. **Stream-Scaled Reward Pruning**: Dual-level evaluation — image reward models (HPSv3, ImageReward, MHP) for frame-level spatial aesthetics + video reward models (VisionReward, VideoAlign, VideoLLaMA3) over sliding 10-chunk windows for temporal coherence
3. **Stream-Scaled Memory Sinking**: Three KV-cache eviction pathways guided by semantic boundary detection — Discard, EMA-Sink (compress trends), Append-Sink (preserve detail)

### Results
- 5s videos: VideoAlign MQ **+79.71%**, VQ **+49.47%** over LongLive baseline
- 30s videos: VideoAlign MQ improves by **11,400%** (-0.002 → 0.226)
- Beats both Best-of-N and Beam Search (passive selection) across all metrics

## Video Background Replacement: Sparkle

[[sources/sparkle-video-bg-replacement|Sparkle (2026)]] advances video editing with **instruction-guided background replacement**:
- **Decoupled guidance**: Separate control paths for foreground preservation and background synthesis
- **Temporal consistency**: New backgrounds maintain coherent motion across frames
- Addresses the gap between style transfer (local editing) and full scene replacement (global synthesis)
- Scalable training data pipeline for background replacement pairs

## High-Resolution Image-to-Video: SwiftI2V

[[sources/swifti2v-highres|SwiftI2V (2026)]] tackles high-resolution (2K) image-to-video generation:
- **Segment-wise generation**: Parallel processing of video segments instead of end-to-end generation
- **Bidirectional context**: Forward and backward information exchange between segments
- Avoids the expense of end-to-end models and the hallucination of cascading super-resolution
- Preserves fine-grained input image details at scale


## Efficient Video Editing: LIVEditor (ISA)

[[sources/lightning-video-editing|LIVEditor (2026)]] tackles the computational bottleneck of in-context learning video editing with **In-context Sparse Attention (ISA)**:

- **Key insight**: Context tokens have systematically lower saliency than source tokens; query sharpness correlates with approximation error
- **Dynamic routing**: High-sharpness queries (low error) → efficient 0-th order Taylor sparse attention; low-sharpness queries → full attention
- **Results**: ~60% attention-module latency reduction while **surpassing** full-attention quality on EditVerseBench, IVE-Bench, VIE-Bench
- **1.7M curated dataset**: Video-to-video editing pairs across 7 categories (style transfer, object manipulation, background changes, etc.)
- Demonstrates that efficient attention is not just for generation but equally critical for editing

## Key Papers
- [[sources/svd|Stable Video Diffusion]] (2023) — Open video generation baseline
- [[sources/cogvideox|CogVideoX]] (2024) — Open text-to-video
- [[sources/seedance|Seedance 1.0]] (2025) — SOTA quality with video RLHF
- [[sources/self-forcing-pp|Self-Forcing++]] (2025) — Minute-scale generation
- [[sources/sparkle-video-bg-replacement|Sparkle]] (2026) — Video background replacement with decoupled guidance
- [[sources/swifti2v-highres|SwiftI2V]] (2026) — High-resolution image-to-video via segment-wise generation
- [[sources/stream-t1|Stream-T1]] (2026) — Active test-time scaling for streaming video generation

## See Also
- [[concepts/diffusion-models|Diffusion Models]]
- [[concepts/rectified-flow|Rectified Flow]]
- [[comparisons/diffusion-architectures|Diffusion Architectures]]