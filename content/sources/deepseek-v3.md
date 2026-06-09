---
type: source
arxiv_id: "2412.19437"
title: "DeepSeek-V3 Technical Report"
authors: ["DeepSeek-AI"]
date: 2024-12-26
org: "DeepSeek"
tags: [moe, architecture, pre-training, mla, frontier-model, 2024]
upvotes: 82
---

# DeepSeek-V3

> A 671B MoE model (37B active/token) that pioneered auxiliary-loss-free load balancing, Multi-head Latent Attention (MLA), and multi-token prediction — trained for just $5.5M, revolutionizing cost-efficient frontier training. 102K+ GitHub stars.

## Key Contributions
- **Multi-head Latent Attention (MLA)**: Compresses KV cache by projecting keys and values into a low-dimensional latent space — dramatically reduces inference memory without quality loss
- **Auxiliary-loss-free load balancing**: Expert routing without auxiliary losses — uses a bias term adjusted per training step, achieving better specialization than loss-based balancing
- **Multi-Token Prediction (MTP)**: Predicts multiple future tokens at each position using sequential modules — densifies training signals and improves data efficiency
- **FP8 mixed-precision training**: Fine-grained FP8 quantization during training (not just inference) — first to validate FP8 at frontier scale
- **$5.5M training cost**: Only 2.788M H800 GPU hours — 10× cheaper than comparable frontier models

## Method
1. **Architecture**: 61 Transformer layers, hidden dim 7168. DeepSeekMoE with 256 routed experts (8 activated per token) + 1 shared expert per layer. Top-K routing with auxiliary-loss-free balancing
2. **MLA**: Instead of storing full K/V heads, projects them into a shared low-rank latent vector. At inference, only the compressed latent needs caching — up to 93% KV cache reduction vs. standard GQA
3. **Auxiliary-loss-free balancing**: Adds a learnable bias term to expert routing scores. Bias is updated based on expert load — overloaded experts get lower bias, underloaded get higher. No auxiliary loss needed in the training objective
4. **Multi-Token Prediction**: Each position predicts the next D tokens (D=2 in practice) via sequential prediction modules. MTP modules share the main model's embedding but have separate output heads. Used as auxiliary training signal
5. **Training**: 14.8T tokens on 2048 H800 GPUs. FP8 for GEMM operations. Pipeline parallelism (16-way) + expert parallelism (64-way). No irrecoverable loss spikes or rollbacks throughout training
6. **Post-training**: SFT on 1.5M curated instances → RL with rule-based + model-based rewards. Uses [[sources/qwen25|YaRN]] for context extension to 128K

## Results
- Outperforms all open-source models; competitive with GPT-4o, Claude 3.5 Sonnet
- MMLU: 88.5, MATH-500: 90.2, HumanEval: 65.2, Codeforces: 51.6 (percentile)
- Training remarkably stable — zero rollbacks during entire 14.8T token run
- MTP improves performance by ~0.5% on benchmarks with negligible cost increase
- MLA reduces KV cache by ~93% vs. standard multi-head attention
- Auxiliary-loss-free model shows greater expert specialization than loss-based baseline

## Models Released
- **DeepSeek-V3** (671B MoE, 37B active) — base model for [[sources/deepseek-r1|DeepSeek-R1]]

## Connections
- Extended by: [[sources/deepseek-r1|DeepSeek-R1]] (reasoning via GRPO on top of V3)
- Builds on: DeepSeek-V2 (introduced MLA/DeepSeekMoE), [[sources/deepseekmath|DeepSeekMath]] (GRPO)
- Related: [[sources/mixtral|Mixtral]] (earlier MoE), [[concepts/mixture-of-experts|MoE]]
- Concepts: [[concepts/mixture-of-experts|Mixture of Experts]], [[concepts/mla|Multi-head Latent Attention]]
- Org: [[entities/orgs/deepseek|DeepSeek]]

## Citation
> DeepSeek-AI, "DeepSeek-V3 Technical Report," arXiv:2412.19437, 2024.
