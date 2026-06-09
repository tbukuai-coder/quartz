---
type: source
arxiv_id: "2605.13779"
title: "MinT: Managed Infrastructure for Training and Serving Millions of LLMs"
authors: ["Song Cao", "Vic Cao", "Andrew Chen", "Kaijie Chen", "Cleon Cheng", "Steven Chiang", "Kaixuan Fan", "Hera Feng", "Huan Feng"]
date: 2026-05-14
org: "MindLab"
tags: [infrastructure, lora, serving, training, scaling, 2026]
upvotes: 219
---

# MinT: Managed Infrastructure for Training and Serving Millions of LLMs

> Managed infrastructure system for LoRA post-training and serving at scale — keeps base models resident, moves lightweight adapter revisions through rollout/update/export/serve/rollback lifecycle, supporting millions of policies over few base deployments.

## Key Contributions
- **Base-model-resident architecture**: keeps expensive base models loaded while cycling lightweight LoRA adapters through training and serving
- **Adapter revision lifecycle**: rollout → update → export → evaluation → serving → rollback — full lifecycle management for adapter policies
- **Multi-architecture support**: handles dense architectures, MoE architectures, MLA attention, and DSA attention
- **Scale-up/down/out**: tensor-parallel deployment, adapter-only handoff, packed MoE tensors
- **Policy catalogs**: manages millions of trained adapter policies across GRPO and other RL methods
- **Eliminates cold loading**: no full-checkpoint materialization; adapters are hot-swapped

## Method
MinT targets settings where many trained policies share a small number of expensive base-model deployments. Instead of materializing each policy as a merged full checkpoint, the system keeps the base model resident on GPUs and moves exported LoRA adapter revisions through a managed lifecycle. Distributed training, serving, scheduling, and data movement are hidden behind a unified service interface. The system supports scale-up (larger models), scale-down (reduced storage via adapter-only handoff), and scale-out (tensor-parallel deployment across policy catalogs).

## Results
- Supports millions of LoRA policies over few base deployments
- Eliminates redundant checkpoint materialization (massive storage savings)
- Enables rapid policy iteration for GRPO-style RL training
- Handles MoE and attention variants (MLA, DSA) at production scale

## Connections
- Builds on: [[sources/lora]], [[concepts/lora-peft]], [[concepts/training-infrastructure]]
- Related: [[sources/llamafactory]], [[concepts/llm-serving]], [[concepts/mixture-of-experts]]
- Enables: [[concepts/grpo]], [[concepts/rlhf]], large-scale RL policy training

## Citation
> Cao et al., "MinT: Managed Infrastructure for Training and Serving Millions of LLMs," arXiv:2605.13779, 2026.
