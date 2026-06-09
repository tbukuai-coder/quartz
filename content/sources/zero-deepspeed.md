---
type: source
arxiv_id: "1910.02054"
title: "ZeRO: Memory Optimizations Toward Training Trillion Parameter Models"
authors: ["Samyam Rajbhandari", "Jeff Rasley", "Olatunji Ruwase", "Yuxiong He"]
date: 2019-10-03
org: "Microsoft DeepSpeed"
tags: [training-infrastructure, distributed-training, efficiency, foundational]
upvotes: 11
---

# ZeRO / DeepSpeed

> The Zero Redundancy Optimizer that eliminates memory redundancy in data-parallel training — enabling 8× larger models with no architecture changes. Built into HF Transformers Trainer and Accelerate. The most widely used distributed training backend in the HF ecosystem.

## Key Contributions
- **Three stages of memory optimization**: Partition optimizer states (Stage 1), gradients (Stage 2), and parameters (Stage 3) across data-parallel ranks
- **Up to 8× memory reduction**: Stage 3 enables training models 8× larger than standard data parallelism
- **No architecture changes**: Works with any model — just change the training configuration
- **ZeRO-Offload / ZeRO-Infinity**: Extend to CPU/NVMe memory for even larger models on limited GPUs

## Method
In standard data-parallel training, every GPU stores a full copy of: model parameters (fp16), gradients (fp16), and optimizer states (fp32 params + fp32 momentum + fp32 variance for Adam). This 3× redundancy wastes memory.

1. **Stage 1 (Optimizer State Partitioning)**: Each GPU stores only 1/N of the optimizer states. All-gather before optimizer step. **4× memory reduction** for mixed-precision Adam
2. **Stage 2 (+ Gradient Partitioning)**: Each GPU stores only 1/N of gradients. Reduce-scatter after backward. **8× memory reduction**
3. **Stage 3 (+ Parameter Partitioning)**: Each GPU stores only 1/N of parameters. All-gather before forward/backward. **Linear memory scaling** — N GPUs train N× larger model
4. **ZeRO-Offload**: Move optimizer states and computations to CPU — train 10B models on a single GPU
5. **ZeRO-Infinity**: Extend offloading to NVMe SSDs — train trillion-parameter models on limited clusters

## Results
- 1T parameter model trained on 1024 GPUs (at time of publication, largest model ever)
- Stage 2: 8× memory reduction, near-linear throughput scaling up to 64 GPUs
- Stage 3: Linear memory scaling — enables models impossible with standard data parallelism
- ZeRO-Offload: Train 10B models on single V100 (32GB)
- Superlinear speedup possible via memory savings → larger batch sizes

## Impact on the Ecosystem
ZeRO/DeepSpeed is the **default distributed training backend** in HF:
- Built into `transformers.Trainer` via `deepspeed` config
- Integrated in `accelerate` library
- Used by TRL for RLHF/DPO/SFT training
- Default recommendation in every HF training tutorial for multi-GPU
- Most open-source LLM training runs use ZeRO Stage 2 or 3

## Connections
- Complementary: [[sources/flash-attention|FlashAttention]] (compute efficiency), [[concepts/lora-peft|LoRA]] (parameter efficiency)
- Used by: Every multi-GPU training job in the HF ecosystem
- Alternative: FSDP (PyTorch native — similar concept, different implementation)
- Concepts: [[concepts/training-infrastructure|Training Infrastructure]]
- Org: [[entities/orgs/microsoft|Microsoft Research]]

## Citation
> Rajbhandari et al., "ZeRO: Memory Optimizations Toward Training Trillion Parameter Models," SC 2020, arXiv:1910.02054.
