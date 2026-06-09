---
type: source
arxiv_id: "2605.12357"
title: "δ-mem: Efficient Online Memory for Large Language Models"
authors: ["Jingdi Lei", "Di Zhang", "Junxian Li", "Weida Wang", "Kaixuan Fan", "Xiang Liu", "Qihan Liu", "Xiaoteng Ma", "Baian Chen", "Soujanya Poria"]
date: 2026-05-13
org: "SUTD / Declare Lab"
tags: [architecture, memory, long-context, attention, 2026]
upvotes: 125
---

# δ-mem: Efficient Online Memory for Large Language Models

> Lightweight associative memory mechanism augmenting frozen LLMs with a compact delta-rule-updated state matrix providing low-rank corrections to attention — enables effective long-term memory without expanding context windows.

## Key Contributions
- **Delta-rule associative memory**: compact fixed-size state matrix updated via delta-rule learning that compresses past information
- **Low-rank attention correction**: memory readout provides corrections to attention computations without modifying the backbone
- **Frozen backbone compatible**: works with any frozen full-attention LLM as a plug-in module
- **Online update**: memory state updates continuously as new tokens arrive, no recomputation needed
- **191 GitHub stars** at Declare Lab

## Method
δ-mem augments a frozen full-attention LLM with a compact online associative memory. The memory is a fixed-size state matrix updated by the delta rule: each new token updates the memory based on prediction error (difference between current attention output and memory readout). At each layer, the memory readout provides a low-rank correction to the standard attention computation, effectively expanding the model's effective context without increasing the actual context window. The memory persists across contexts, enabling long-term agent memory.

## Results
- Significant improvements on memory-heavy benchmarks (MemoryAgentBench, LoCoMo)
- Effective long-term information retention without context window expansion
- Minimal parameter overhead (fixed-size state matrix)
- Works as drop-in enhancement for existing frozen models

## Connections
- Builds on: [[sources/mia-signature]], [[concepts/long-context]], [[concepts/kv-cache]]
- Related: [[sources/hrm-text]], [[sources/mamba]], [[concepts/state-space-models]]
- Bridges: attention-based models with recurrent memory mechanisms

## Citation
> Lei et al., "δ-mem: Efficient Online Memory for Large Language Models," arXiv:2605.12357, 2026.
