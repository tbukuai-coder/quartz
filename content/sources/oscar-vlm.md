---
type: source
arxiv_id: "2605.00323"
title: "Online Self-Calibration Against Hallucination in Vision-Language Models"
authors: ["Unknown"]
date: 2026-05-02
org: "Unknown"
tags: [vision-language-models, hallucination, preference-optimization, dpo, mcts, self-improvement, 2026]
upvotes: 1
---

# OSCAR: Online Self-Calibration Against Hallucination in VLMs

> A novel training paradigm (OSCAR) that exploits the Generative-Discriminative Gap in LVLMs — using MCTS with a Dual-Granularity Reward Mechanism to enable lookahead that suppresses early tokens risking downstream hallucinations, updated via DPO.

## Key Contributions

- **Supervision-Perception Mismatch identified**: Offline distillation from stronger teachers forces weaker students to reproduce fine-grained visual details beyond their perceptual capacity — paradoxically *increasing* hallucination rates
- **Generative-Discriminative Gap**: LVLMs perform considerably better on discriminative verification tasks ("does object X exist?") than on open-ended generation — latent self-verification capacity is underutilized during generation
- **OSCAR framework**: Online preference learning via MCTS + Dual-Granularity Reward + DPO updates:
  - **Node-level reward**: Discriminative verification using negative-response probability as process reward
  - **Trajectory-level reward**: Gated Outcome Reward evaluates quality only if faithfulness check passes
  - **Two-granularity preference pairs**: Global path comparison + sibling comparison from MCTS tree
- **Continuous self-improvement**: Each DPO iteration updates the model, which then generates new preference data through MCTS

## Results

- **SOTA on hallucination benchmarks** while simultaneously improving general multimodal capabilities
- Offline teacher-distilled data paradoxically increases hallucination rates for LLaVA-1.5-7B (validated empirically)
- Model learns to see rather than guess through online self-calibration

## Connections
- Builds on: [[sources/dpo]], [[sources/grpo]], [[concepts/rlhf]], [[sources/llava]]
- Related concepts: [[concepts/vision-language-models]], [[concepts/llm-safety]]
- Related papers: [[sources/edit-r1]], [[sources/reasoning-vectors]], [[sources/compliance-vs-sensibility]]
- Cited by / Influenced: VLM hallucination mitigation, online preference learning, self-improving vision models

## Citation
> "Online Self-Calibration Against Hallucination in Vision-Language Models," arXiv:2605.00323, 2026.
