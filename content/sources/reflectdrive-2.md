---
type: source
arxiv_id: "2605.04647"
title: "ReflectDrive-2: RL-Aligned Self-Editing for Goal-Conditioned Masked Diffusion Driving Planners"
authors: null
venue: "arXiv preprint"
year: 2026
date: "2026-05"
upvotes: 6
tags: [autonomous-driving, diffusion, vla, reinforcement-learning, self-correction, robotics]
github: null
---

# ReflectDrive-2: RL-Aligned Self-Editing for Goal-Conditioned Masked Diffusion Driving Planners

> A reflective masked-diffusion VLA planner for autonomous driving that plans through a **decision–draft–reflect** process: goal-point posterior proposes behavior hypotheses, masked discrete diffusion drafts editable trajectories, and **AutoEdit** rewrites drafts in-place — all co-trained via RL over the full rollout.

## Key Contributions

1. **Goal-conditioned masked-diffusion planning**: Goal-point posterior exposes behavior-level hypotheses (lane keeping, yielding, overtaking, changing lanes); masked discrete diffusion drafts trajectories for each; AutoEdit rewrites in the same token space
2. **Reward-coupled AutoEdit**: RL over the full draft-and-edit rollout co-adapts drafter and editor — the drafter learns to emit revisable drafts, the editor learns corrections that improve closed-loop reward
3. **Efficient reflective decoding**: Shared-prefix KV cache, Alternating Step Decode (ASD) reusing AutoEdit across frames, fused CUDA unmasking — **31.8 ms/frame on NVIDIA Thor**
4. **State-of-the-art camera-only performance**: **91.0 PDMS** on NAVSIM (best-of-6 oracle: **94.8 PDMS**, matching human reference)

## Method

### Architecture
- **Inputs**: Panoramic cameras + route/navigation instruction tokens + ego state
- **Outputs**: Discrete trajectory tokens (8 waypoints = 16 coordinate tokens)
- **Backbone**: 0.7B masked-diffusion language model + 0.1B ViT visual encoder
- **Training**: Supervised fine-tuning → reinforcement fine-tuning with PDMS reward

### Three-Stage Inference Process

1. **Decision**: Goal-point posterior samples candidate behavioral hypotheses via top-k + non-maximum suppression
2. **Draft**: Masked discrete diffusion parallel-decodes trajectory for each goal hypothesis
3. **Reflect**: AutoEdit rewrites trajectory tokens in-place conditioned on the draft

### AutoEdit: Self-Correction Mechanism

**Pretraining**: Structure-aware perturbations along longitudinal (speed misjudgment) and lateral (heading drift) failure axes of imitation learning

**RL Co-Training**: Single terminal reward assigns policy-gradient credit to both drafting and editing transitions
- Before RL: inference-time AutoEdit contributes **+0.3 PDMS** at most
- After RL: same AutoEdit contributes **+1.9 PDMS**
- **Mechanism**: Drafter learns to emit token distributions whose post-edit score exceeds pre-edit; editor learns corrections toward closed-loop reward

### Efficient Runtime Stack

| Component | Technique | Benefit |
|---|---|---|
| **Shared-prefix KV cache** | Reuse across decision/draft/reflect phases | Eliminates redundant prefill |
| **Alternating Step Decode (ASD)** | Reuse AutoEdit as temporal refiner across frames | Smooth temporal consistency |
| **Fused on-device unmasking** | Custom CUDA kernel | Speed |

**Result**: 31.8 ms average latency on NVIDIA Thor with near-lossless planning quality

## Results

### NAVSIM Closed-Loop Planning (Camera-Only)

| Method | Input | NC | DAC | TTC | Comf. | EP | **PDMS** |
|---|---|---|---|---|---|---|---|
| UniAD | Cam | 97.8 | 91.9 | 92.9 | 100.0 | 78.8 | 83.4 |
| Hydra-MDP | C+L | 98.3 | 96.0 | 94.6 | 100.0 | 78.7 | 86.5 |
| DiffusionDrive | C+L | 98.2 | 96.2 | 94.7 | 100.0 | 82.2 | 88.1 |
| GoalFlow | C+L | 98.4 | 98.3 | 94.6 | 100.0 | 85.0 | 90.3 |
| AutoVLA | Cam | 98.4 | 95.6 | 98.0 | 99.9 | 81.9 | 89.1 |
| DriveVLA-W0 | Cam | 98.7 | 99.1 | 95.3 | 99.3 | 83.3 | 90.2 |
| ReCogDrive | Cam | 97.9 | 97.3 | 94.9 | 100.0 | 87.3 | 90.8 |
| **ReflectDrive-2** | **Cam** | **97.3** | **98.1** | **92.5** | **100.0** | **89.4** | **91.0** |

- **Camera-only** 91.0 PDMS > all camera-only VLA peers (89.1–90.8)
- **Best-of-6 oracle**: 94.8 PDMS = NAVSIM human reference
- Largest gain in **Ego Progress (EP = 89.4)** — significant progress improvement while maintaining DAC (98.1) and comfort (100.0)

### Decision Diversity
Goal points are genuine behavior hypotheses, not sampling noise:
- Turning scenes: different goal points realize different curve lines, some respecting drivable boundaries better
- Interaction scenes: longitudinally and laterally distinct behaviors (keep lane / change lane / adjust speed)

### Reflection Visualization
- AutoEdit pulls trajectories back into drivable area
- Adjusts plans around nearby agents
- Revisions are structured rewrites in the same token space, not cosmetic smoothing

## Connections

- [[sources/continuous-time-distribution-matching|Continuous-Time DMD]] — Both use diffusion for generation; ReflectDrive-2 applies masked discrete diffusion to driving trajectories
- [[sources/marble|MARBLE]] — Multi-reward RL for diffusion; ReflectDrive-2 uses single PDMS reward but couples drafter+editor
- [[sources/trust-imagination-wam|When to Trust Imagination]] — Adaptive action execution for robotics; ReflectDrive-2 adaptive reflection for driving
- [[sources/exoactor|ExoActor]] — Video-to-control for humanoid robots; ReflectDrive-2 for autonomous driving
- [[concepts/agents|Agents & Tool Use]] — VLA as embodied agent with self-correction
- [[concepts/diffusion-models|Diffusion Models]] — Masked discrete diffusion applied to trajectory planning
