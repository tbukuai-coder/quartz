---
type: source
arxiv_id: "2404.14619"
title: "OpenELM: An Efficient Language Model Family with Open-source Training and Inference Framework"
authors: ["Sachin Mehta", "Mohammad Hossein Sekhavat", "Qingqing Cao", "Maxwell Horton", "Yanzi Jin"]
date: 2024-04-22
org: "Apple"
tags: [small-model, open-science, efficiency, pre-training, 2024]
upvotes: 126
---

# OpenELM

> Apple's fully open language model family using layer-wise scaling to efficiently allocate parameters, released with training code, logs, and checkpoints.

## Key Contributions
- Introduced **layer-wise scaling** for Transformer models — allocating different numbers of attention heads and FFN dimensions per layer for better parameter efficiency
- Achieved **2.36% accuracy improvement** over OLMo-1B with 2× fewer pre-training tokens
- Released **complete open-source framework**: training code, evaluation framework, model weights, training logs, checkpoints, and data recipes
- Provided **Apple MLX** integration for efficient on-device inference on Apple Silicon
- Demonstrated that architecture-level efficiency matters — not just data or scale

## Method
**Layer-wise scaling**: Instead of using uniform dimensions across all Transformer layers, OpenELM varies the number of attention heads and FFN width per layer. Earlier layers use fewer parameters (simpler features), later layers get more (complex reasoning). This is parameterized by a scaling factor α that controls the parameter distribution curve.

Architecture uses RoPE, SwiGLU, RMSNorm, GQA — the standard [[sources/llama|LLaMA template]], but with the layer-wise scaling innovation. Four model sizes: **270M, 450M, 1.1B, 3B** parameters.

**Training**: Pre-trained on public datasets including RefinedWeb, RedPajama, The Pile, Dolma. ~1.8T tokens for the largest model.

## Results
- **OpenELM-1.1B** outperforms OLMo-1B (avg 49.0 vs 46.6 on standard benchmarks) using 2× fewer tokens
- **OpenELM-3B** competitive with Phi-2 (2.7B) on some benchmarks
- Layer-wise scaling consistently improves over uniform baselines at all scales (270M–3B)
- Efficient inference on Apple Silicon via MLX

## Datasets Used
- [[entities/datasets/refinedweb|RefinedWeb]], [[entities/datasets/redpajama|RedPajama]], The Pile, [[entities/datasets/dolma|Dolma]]

## Models Released
- OpenELM 270M, 450M, 1.1B, 3B (open weights + code + logs)

## Connections
- **Builds on**: [[sources/llama|LLaMA]] (architecture), [[sources/olmo|OLMo]] (open-science benchmark)
- **Related**: [[entities/models/smollm|SmolLM]] (small models), [[sources/phi-3|Phi-3]] (efficient small models)
- **Related concepts**: [[concepts/pre-training|Pre-training]], [[concepts/transformer-architecture|Transformer Architecture]]
- **Comparison**: [[comparisons/small-language-models|Small Language Models]] — part of the sub-3B model landscape
- **Related orgs**: Apple (first major open model release)

## Citation
> Mehta et al., "OpenELM: An Efficient Language Model Family with Open-source Training and Inference Framework," arXiv:2404.14619, 2024.
