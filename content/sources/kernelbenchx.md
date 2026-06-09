---
type: source
arxiv_id: "2605.04956"
title: "KernelBench-X: A Comprehensive Benchmark for Evaluating LLM-Generated GPU Kernels"
authors: ["Han Wang", "Jintao Zhang", "Kai Jiang", "Haoxu Wang", "Jianfei Chen", "Jun Zhu"]
date: 2026-05
tags: [code-generation, gpu-kernels, triton, benchmarking, llm-coding, hardware-efficiency]
upvotes: 1
---

# KernelBench-X: A Comprehensive Benchmark for Evaluating LLM-Generated GPU Kernels

> KernelBench-X systematically evaluates LLM-generated Triton kernels across 176 tasks in 15 categories, revealing that task structure impacts correctness more than method design, and iterative refinement improves correctness at the expense of performance.

## Key Contributions
- Presents KernelBench-X, a comprehensive benchmark with 176 tasks across 15 categories for evaluating LLM-generated GPU kernels
- Systematically compares five representative LLM-based kernel generation methods
- Reveals three main findings:
  1. **Task structure determines correctness more than method design**: The inherent complexity and structure of the task matters more than the specific generation approach
  2. **Iterative refinement improves correctness at the expense of performance**: Self-correction loops help generate correct kernels but often sacrifice speed
  3. **Correctness does not guarantee efficiency**: A kernel can be correct but significantly slower than hand-optimized alternatives
- Evaluates compile rate, speedup, and numerical precision across quantization and other workloads

## Method
The benchmark design:
1. **176 tasks in 15 categories**: Covers diverse GPU kernel workloads including matrix operations, reduction, scan, attention, quantization, etc.
2. **Five representative methods compared**: Different prompting strategies and code generation approaches
3. **Metrics**: Compile rate (does it compile?), correctness (does it produce correct output?), speedup (is it fast?), numerical precision
4. **Iterative refinement analysis**: Measures how self-correction loops affect correctness vs. performance tradeoffs

## Results
- Task structure is the dominant factor for correctness, not the specific LLM prompting strategy
- Iterative self-correction improves compile rate and correctness but degrades performance optimization
- Correctness and efficiency are largely uncorrelated — many correct kernels are far from optimal
- Quantization kernels are particularly challenging for LLM generation

## Datasets Used
- 176 kernel generation tasks across 15 categories

## Models Released
- GitHub: https://github.com/BonnieW05/KernelBenchX (14 stars)

## Connections
- Related: [[sources/starcoder]] — code generation models
- Related: [[sources/starcoder-2]] — advanced code generation
- Related: [[sources/codeact]] — code as actions for LLM agents
- Related concept: [[concepts/agents]], code generation

## Citation
> Wang et al., "KernelBench-X: A Comprehensive Benchmark for Evaluating LLM-Generated GPU Kernels," arXiv:2605.04956, 2026.
