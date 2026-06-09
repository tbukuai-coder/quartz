---
type: source
arxiv_id: "2605.00781"
title: "Map2World: Segment Map Conditioned Text to 3D World Generation"
authors: ["Jaeyoung Chung", "Suyoung Lee", "Jianfeng Xiang", "Jiaolong Yang", "Kyoung Mu Lee"]
date: 2026-05-03
org: "Seoul National University"
tags: [3d-generation, world-generation, diffusion, vision, conditional-generation, 2026]
upvotes: 4
---

# Map2World: Segment Map Conditioned 3D World Generation

> A text-conditioned 3D world generation framework that generates globally coherent, high-resolution 3D scenes from user-defined segment maps of arbitrary shapes — not limited to grid layouts.

## Key Contributions

- **Flexible segment map conditioning**: Generates 3D worlds from any user-defined segment maps with arbitrary shapes and scales, not limited to grid-based layouts
- **Multi-diffusion strategy in structured latent space**: Coordinates overlapping diffusion windows to preserve TRELLIS latent prior while enabling seamless connections beyond individual cube boundaries
- **Consistent detail enhancement**: Adds fine details to assets while preserving overall global structure and scale consistency
- **Domain-generalized world generation**: Leverages powerful 3D asset generator priors (TRELLIS) for robust generation across domains with limited data

## Method

Builds on TRELLIS and addresses key limitations of prior modular approaches:
1. **Contextual disconnectedness**: Adjacent assets lack relationships in prior grid-based methods
2. **Object scale inconsistencies**: Different assets appear at incompatible scales
3. **Grid layout constraints**: Real-world district boundaries are irregularly shaped

Uses multi-diffusion in structured latent space to coordinate overlapping windows, supporting progressive generation at arbitrary resolution while maintaining coherence across local neighborhoods.

## Results

- Significantly improves structural fidelity and perceptual realism over modular baselines
- Supports flexible semantic map conditioning without additional training
- Scenes maintain coherence across boundaries and scales

## Connections
- Builds on: [[sources/trellis]] (implied, TRELLIS foundation), [[concepts/diffusion-models]]
- Related concepts: [[concepts/video-generation]], [[concepts/multimodal-models]]
- Related papers: [[sources/unividx]], [[sources/seedance]], [[sources/cogvideox]]
- Cited by / Influenced: 3D scene generation, world modeling, embodied AI environments

## Citation
> Chung et al., "Map2World: Segment Map Conditioned Text to 3D World Generation," arXiv:2605.00781, 2026.
