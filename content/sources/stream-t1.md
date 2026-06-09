---
type: source
arxiv_id: "2605.04461"
title: "Stream-T1: Test-Time Scaling for Streaming Video Generation"
authors:
  - Yijing Tu
  - Shaojin Wu
  - Mengqi Huang
  - Wenchuan Wang
  - Yuxin Wang
  - Chunxiao Liu
  - Zhendong Mao
venue: arXiv
year: 2026
month: 5
date: "2026-05"
upvotes: 97
tags:
  - video-generation
  - test-time-scaling
  - diffusion-models
  - streaming
  - temporal-consistency
github: https://github.com/FrameX-AI/Stream-T1
stars: 22
---

# Stream-T1: Test-Time Scaling for Streaming Video Generation

## One-Line Summary

Active test-time scaling framework for streaming video generation that dynamically refines latent noise and context memory to achieve state-of-the-art temporal consistency and visual fidelity in long-form videos.

## Key Contributions

1. **First comprehensive TTS framework for streaming video generation** — Shifts test-time scaling from global diffusion to chunk-level autoregressive synthesis with few denoising steps (e.g., 4 per chunk), dramatically reducing candidate exploration costs.
2. **Stream-Scaled Noise Propagation** — Actively refines initial latent noise of each chunk using historically proven high-quality trajectories via spherical interpolation, anchoring exploration space for smooth temporal transitions.
3. **Stream-Scaled Reward Pruning** — Evaluates chunk candidates with a dual-level framework balancing local spatial aesthetics (image reward models: HPSv3, ImageReward, MHP) and global temporal coherence (video reward models: VisionReward, VideoAlign, VideoLLaMA3 over sliding 10-chunk windows).
4. **Stream-Scaled Memory Sinking** — Dynamically routes evicted KV-cache context through three pathways (Discard, EMA-Sink, Append-Sink) via semantic boundary detection, decoupling short-term continuity from long-term memory preservation.

## Method

Built on [[concepts/diffusion-models|streaming video diffusion]] (LongLive / Wan2.1-T2V-1.3B), Stream-T1 operates through three sequential stages per chunk:

### Stage 1: Noise Propagation
Rather than sampling initialization noise from $\mathcal{N}(\mathbf{0}, \mathbf{I})$, the current chunk's noise is constructed via spherical interpolation with the optimal noise from the preceding chunk:
$$x_T^n = \beta x_T^{n-1} + \sqrt{1-\beta^2}\,\epsilon, \quad \epsilon \sim \mathcal{N}(\mathbf{0}, \mathbf{I})$$
where $\beta \in (-1, 1)$ controls temporal correlation. This preserves the marginal Gaussian distribution while establishing temporal dependency.

### Stage 2: Reward Pruning
A **Long-Short Combined Reward** balances:
- **Short-level**: Image reward models (HPSv3, ImageReward, MHP) for frame-level spatial aesthetics
- **Long-level**: Video reward models (VisionReward, VideoAlign, VideoLLaMA3) over sliding windows of 10 chunks for temporal coherence

Suboptimal branches are pruned; only optimal trajectories propagate forward.

### Stage 3: Memory Sinking
The KV-cache eviction strategy dynamically selects among:
- **Discard**: Remove context entirely
- **EMA-Sink**: Exponential moving average compression (preserves long-term trends)
- **Append-Sink**: Append to persistent memory buffer (preserves detailed context)

Selection is guided by semantic boundary detection (reward feedback) to decouple short-term continuity from long-term preservation.

## Results

Evaluated on 5s (VBench, 946 prompts) and 30s (MovieGen, 128 prompts) video generation at 16 FPS, 832×480 resolution.

### 5s Video Generation (vs. CausVid, Self-Forcing, LongLive)
| Metric | Stream-T1 Gain |
|---|---|
| Subject Consistency | +0.26% |
| Background Consistency | +0.28% |
| Motion Smoothness | +0.03% |
| Imaging Quality | +0.2% |
| Aesthetic Quality | +1.07% |
| VideoAlign VQ | **+49.47%** |
| VideoAlign MQ | **+79.71%** |
| VideoAlign TA | +9.39% |

### 30s Video Generation
Stream-T1 achieves best scores on **6 of 8 metrics** including Subject Consistency (98.43), Background Consistency (97.18), Motion Smoothness (99.03), and Aesthetic Quality (62.11). VideoAlign MQ improves by **11,400%** over LongLive baseline (-0.002 → 0.226).

### vs. Standard TTS Methods
Compared to Best-of-N and Beam Search (passive selection paradigms), Stream-T1's **active optimization paradigm** achieves SOTA across all evaluative metrics by dynamically refining latent noise and context memory rather than merely selecting from a fixed pool.

## Connections

- **Temporal Guidance**: Unlike prior TTS methods (ImagerySearch) that denoise entire videos simultaneously in a global high-dimensional space, Stream-T1's chunk-level synthesis enables fine-grained temporal correction without rejecting entire sequences.
- **Memory Management**: Extends [[concepts/kv-cache|KV-cache]] strategies from long-context LLMs to video diffusion, with semantic-aware eviction (similar to [[sources/learning-while-deploying|Learning while Deploying]]'s DIVL for VLA policies).
- **Reward Engineering**: Dual-level reward framework parallels [[sources/marble|MARBLE]]'s multi-reward gradient harmonization, but applied to temporal rather than spatial dimensions.
- **Streaming Architecture**: Builds on LongLive's autoregressive chunk generation with self-forcing, but adds active TTS optimization rather than passive conditioning.

## Citation

```bibtex
@article{tu2026streamt1,
  title={Stream-T1: Test-Time Scaling for Streaming Video Generation},
  author={Tu, Yijing and Wu, Shaojin and Huang, Mengqi and Wang, Wenchuan and Wang, Yuxin and Liu, Chunxiao and Mao, Zhendong},
  journal={arXiv preprint arXiv:2605.04461},
  year={2026}
}
```

---
*Ingested in Batch 26 (2026-05-05)* | [[index]] | [[concepts/video-generation]] | [[concepts/diffusion-models]] | [[concepts/test-time-compute]]