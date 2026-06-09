---
type: source
arxiv_id: "2209.03003"
title: "Flow Straight and Fast: Learning to Generate and Transfer Data with Rectified Flow"
authors: ["Xingchao Liu", "Chengyue Gong", "Qiang Liu"]
date: 2022-09-07
org: "UT Austin"
tags: [generative-modeling, ode, diffusion-models, rectified-flow, foundational]
upvotes: 3
---

# Rectified Flow

> Rectified flow learns an ODE that transports between two distributions along straight paths, enabling high-quality generation in as few as one Euler step.

## Key Contributions
- Introduced **rectified flow**, an ODE-based generative model that learns straight-line paths between noise and data distributions
- Proved that **rectification** (iteratively retraining on the flow's own couplings) provably reduces transport costs and straightens trajectories
- Demonstrated **one-step generation** — nearly straight flows produce high-quality images with a single Euler discretization step
- Unified generative modeling, image-to-image translation, and domain adaptation under one framework
- Showed theoretical equivalence: diffusion model probability flow ODEs are a special case (nonlinear rectified flow)

## Method
Rectified flow defines a forward process as a **linear interpolation** X_t = t·X_1 + (1-t)·X_0 between noise X_1 and data X_0. A neural network v_Θ is trained to predict the velocity field by minimizing a simple regression loss: E[||v_Θ(X_t, t) - (X_1 - X_0)||²].

The key insight is that straight paths are optimal — they're the shortest paths between two points and can be simulated exactly without time discretization. **Reflow** recursively applies rectification: given a trained flow, generate new (X_0, X_1) pairs by running the ODE, then retrain on these pairs. Each reflow iteration provably straightens the paths further.

Unlike diffusion models that require 50–1000 discretization steps, a sufficiently rectified flow needs only 1–2 steps.

## Results
- **CIFAR-10**: FID 4.85 (1-step), 2.58 (2-reflow), competitive with diffusion models using 100× fewer steps
- **Image generation**: High-quality 256×256 generation on LSUN, CelebA-HQ
- **Image-to-image translation**: Competitive with CycleGAN on unpaired translation tasks
- **Domain adaptation**: Improved downstream classifier accuracy via data transport

## Datasets Used
- CIFAR-10, LSUN (Bedroom, Church), CelebA-HQ, AFHQ

## Connections
- **Foundational for**: [[sources/sd3|SD3 / Rectified Flow Transformers]], FLUX, [[concepts/rectified-flow|Rectified Flow / Flow Matching]]
- **Builds on**: Score-based generative models (Song et al.), Normalizing flows, Optimal transport theory
- **Related concepts**: [[concepts/diffusion-models|Diffusion Models]], [[concepts/rectified-flow|Rectified Flow]]
- **Influenced**: Stable Diffusion 3, FLUX.1, all modern flow-matching models

## Citation
> Liu et al., "Flow Straight and Fast: Learning to Generate and Transfer Data with Rectified Flow," arXiv:2209.03003, 2022.
