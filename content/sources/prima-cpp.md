---
type: source
arxiv_id: "2504.08791"
title: "Prima.cpp: Speeding Up 70B-Scale LLM Inference on Low-Resource Everyday Home Clusters"
authors: ["Zonghang Li", "Tao Li", "Wenjiao Feng", "Mohsen Guizani", "Hongfang Yu"]
date: 2025-04-08
org: "UESTC / HBKU"
tags: [inference, distributed, efficiency, on-device, 2025]
upvotes: 140
---

# Prima.cpp

> A distributed inference system that runs 70B-scale LLMs on everyday home devices with mixed CPUs/GPUs, insufficient RAM/VRAM, slow disks, and Wi-Fi links, achieving 5–17× lower latency than llama.cpp, exo, and dllama.

## Key Contributions
- Introduces **Pipelined-Ring Parallelism (PRP)** — a new parallelism strategy that overlaps disk I/O with compute and communication, solving the prefetch-release conflict in mmap-based model offloading
- Proposes **Halda** — a heterogeneity-aware scheduler that co-optimizes per-device CPU/GPU workloads and device selection under RAM/VRAM constraints via integer linear programming
- Achieves **674 ms/token** for a 70B model and **26 tokens/s** for a 32B model with speculative decoding on four consumer home devices connected via Wi-Fi
- Delivers **5–17× lower TPOT** than llama.cpp, exo, and dllama while remaining OOM-free with <6% memory pressure
- Supports fine-grained model sizes from 8B to 70B across heterogeneous OSs (Linux, macOS, Android)

## Method
**Problem**: Existing on-device inference systems either require GPU clusters (too expensive for homes) or can only handle small models. Home clusters have mixed devices, low memory, slow storage, and Wi-Fi networking.

**Pipelined-Ring Parallelism (PRP)**:
- Standard pipeline parallelism requires sufficient aggregated RAM — not available in homes
- PRP uses a "layer window" approach: each device loads only a few layers at a time, computes them, and cycles to the next batch
- Solves the **prefetch-release conflict** where the OS's mmap prefetcher loads layer N+1 while layer N is still in use, causing thrashing
- Ring topology allows overlapping: while device 1 computes, device 2 prefetches, device 3 communicates

**Halda scheduler**:
- Formulates layer-to-device assignment as an optimization problem
- Considers each device's RAM, VRAM, disk speed, CPU/GPU compute, and network bandwidth
- Solves via enumeration over valid layer window sizes + integer linear programming
- Automatically selects the optimal subset of devices (sometimes fewer devices = faster)

**Speculative decoding support**: Draft model (0.5–3B) runs as standalone process on the head device. Draft generates 5 candidate tokens; target model verifies in one forward pass.

## Results
Tested on four consumer devices connected via Wi-Fi (320–610 Mbps):
- **70B model**: 674 ms/token TPOT with <6% memory pressure
- **32B model**: 26 tokens/s with speculative decoding
- **vs. llama.cpp**: 5× lower TPOT
- **vs. exo**: 10–17× lower TPOT, plus no OOM
- **vs. dllama**: 8–15× lower TPOT
- Supports Llama 1/3, Qwen 2.5, QwQ, DeepSeek-R1

## Connections
- Related to: [[sources/vllm|vLLM]] (inference optimization), [[sources/sglang|SGLang]] (serving)
- Extends: [[concepts/speculative-decoding]] for home clusters
- Related concepts: [[concepts/llm-serving]], [[concepts/quantization]], [[concepts/kv-cache]]

## Citation
> Li et al., "Prima.cpp: Speeding Up 70B-Scale LLM Inference on Low-Resource Everyday Home Clusters," arXiv:2504.08791, 2025.
