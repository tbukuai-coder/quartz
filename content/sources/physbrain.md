---
type: source
arxiv_id: "2605.15298"
title: "PhysBrain 1.0 Technical Report"
authors: ["PhysBrain Team"]
date: 2026-05-18
org: "PhysBrain"
tags: [robotics, vla, embodied-ai, physical-commonsense, multimodal, 2026]
upvotes: 143
---

# PhysBrain 1.0: Vision-Language-Action with Physical Commonsense

> Leverages human egocentric video to generate physical commonsense supervision for VLA models, achieving SOTA on embodied control benchmarks through capability-preserving adaptation.

## Key Contributions
- **Physical commonsense supervision from egocentric video**: generates training signal about physical properties (weight, friction, fragility) from human manipulation videos without manual annotation
- **Capability-preserving adaptation**: maintains pre-trained VLM understanding while adding embodied control capabilities
- **Multimodal QA + embodied control**: jointly trained on multimodal QA benchmarks and embodied control tasks
- Achieves SOTA on embodied control benchmarks while maintaining strong VLM performance

## Method
PhysBrain 1.0 extracts physical commonsense knowledge from large-scale human egocentric videos — observing how humans handle objects reveals implicit physical properties. This supervision is combined with standard VLA training. A capability-preserving adaptation strategy ensures the model retains its pre-trained vision-language understanding while acquiring new embodied skills, avoiding catastrophic forgetting of general knowledge.

## Results
- SOTA on embodied control benchmarks
- Maintains competitive performance on multimodal QA benchmarks (no catastrophic forgetting)
- Successfully transfers physical commonsense from egocentric observation to robotic manipulation

## Connections
- Builds on: [[sources/learning-while-deploying]], [[sources/trust-imagination-wam]], [[sources/exoactor]]
- Related: [[concepts/multimodal-models]], [[concepts/agents]], [[concepts/vision-language-models]]
- Extends: VLA models with physical commonsense reasoning

## Citation
> PhysBrain Team, "PhysBrain 1.0 Technical Report," arXiv:2605.15298, 2026.
