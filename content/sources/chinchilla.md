---
type: source
arxiv_id: "2203.15556"
title: "Training Compute-Optimal Large Language Models"
authors: ["Jordan Hoffmann", "Sebastian Borgeaud", "Arthur Mensch", "Elena Buchatskaya", "Trevor Cai", "Eliza Rutherford"]
date: 2022-03-29
org: "DeepMind"
tags: [scaling-laws, pre-training, foundational, compute-optimal]
upvotes: 11
---

# Chinchilla — Compute-Optimal Scaling Laws

> Demonstrated that LLMs were massively undertrained: for a fixed compute budget, model size and training tokens should scale equally. Chinchilla (70B, 1.4T tokens) beats Gopher (280B, 300B tokens) on all benchmarks. The universal baseline for all modern LLM training decisions.

## Key Contributions
- **Compute-optimal scaling law**: For a fixed FLOP budget, model parameters N and training tokens D should scale roughly equally (N ∝ D)
- **"Chinchilla-optimal"** became the standard term: GPT-3 and Gopher were 4–5× undertrained
- **Chinchilla model**: 70B params trained on 1.4T tokens beats 280B Gopher trained on 300B tokens — 4× smaller, uniformly better
- **400+ model training runs**: Comprehensive experiments from 70M to 16B params, 5B to 500B tokens

## Method
Three complementary approaches to determine optimal N/D trade-off:
1. **Fixed model sizes, varying tokens**: Train each size on increasing data → find loss-minimizing token count per size
2. **IsoFLOP curves**: For each FLOP budget, train many (N, D) combinations → find the minimum loss point
3. **Parametric loss function**: Fit L(N, D) = E + A/N^α + B/D^β to all 400+ runs → derive optimal N*(C) and D*(C)

All three approaches converge: **N and D should scale equally with compute**.

## Results
- **Chinchilla (70B, 1.4T tokens)**: Beats Gopher (280B), GPT-3 (175B), Jurassic-1 (178B), Megatron-Turing NLG (530B) on MMLU, MATH, BIG-bench, and more
- **4× smaller model, uniformly better** — proves scaling tokens is as important as scaling parameters
- Prior models were 4–5× undertrained relative to their parameter count
- Established that a 67B model needs ~1.5T tokens for compute-optimal training

## Impact on the Ecosystem
Chinchilla reshaped all subsequent LLM training:
- [[sources/llama|LLaMA]] explicitly follows Chinchilla scaling (7B on 1T tokens)
- [[sources/smollm2|SmolLM2]] goes further — 1.7B on 11T tokens (6500:1 ratio, "over-training")
- [[sources/qwen25|Qwen2.5]] trains on 18T tokens — intentional over-training for smaller deployment
- Every model in the wiki implicitly references this paper's compute-optimal framework

## Connections
- Extends: Kaplan et al. (2020) scaling laws (showed different, model-favoring ratio)
- Used by: [[sources/llama|LLaMA]], [[sources/smollm2|SmolLM2]], [[sources/qwen25|Qwen2.5]], [[sources/phi-4|Phi-4]], all open models
- Concepts: [[concepts/scaling-laws|Scaling Laws]], [[concepts/pre-training|Pre-training]]

## Citation
> Hoffmann et al., "Training Compute-Optimal Large Language Models," arXiv:2203.15556, 2022.
