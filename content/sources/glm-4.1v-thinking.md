---
type: source
arxiv_id: "2507.01006"
title: "GLM-4.1V-Thinking: Towards Versatile Multimodal Reasoning with Scalable Reinforcement Learning"
authors: ["Wenyi Hong", "Wenmeng Yu", "Xiaotao Gu", "Guo Wang", "et al."]
date: 2025-07-01
org: "Zhipu AI"
tags: [vision-language, multimodal, reinforcement-learning, reasoning, rlvr, rlhf, 2025]
upvotes: 255
---

# GLM-4.1V-Thinking

> A family of vision-language models achieving SOTA multimodal reasoning through Reinforcement Learning with Curriculum Sampling (RLCS) across 42 benchmarks.

## Key Contributions
- Introduces **Reinforcement Learning with Curriculum Sampling (RLCS)** — a multi-domain RL framework that progressively adjusts task difficulty during training to unlock the full potential of VLMs
- Demonstrates that **a weak verifier in any single domain can collapse the entire multi-domain RL training** — a critical finding for scaling RL across diverse multimodal tasks
- GLM-4.1V-9B-Thinking (9B) **outperforms the much larger Qwen2.5-VL-72B on 29 benchmarks** — showing small-model quality with the right training recipe
- GLM-4.5V (106B, 12B activated MoE) achieves **SOTA on nearly all tasks among open-source models** and competes with Gemini-2.5-Flash on coding and GUI agents
- Open-sources both the 9B and 106B (A12B) models

## Method
The training pipeline has three stages:

1. **Pre-training**: Uses AIMv2-Huge as the vision encoder with an MLP adapter projecting into a large language model decoder. Pre-trains on large-scale caption data, academic corpora, and knowledge-rich interleaved datasets. Includes a long-context continual training phase extending to 32K tokens.
2. **Supervised Fine-Tuning (SFT)**: Curates a long chain-of-thought reasoning dataset as a bridge to RL. Full-parameter fine-tuning with 32K sequence length and batch size of 32. Includes both multimodal and text-only reasoning data.
3. **Reinforcement Learning (RLCS)**: The core innovation. Combines RLVR (verifiable rewards) and RLHF (model-based rewards) across all multimodal domains: STEM, grounding, OCR, video understanding, GUI agents, charts, documents, and logical reasoning. Uses GRPO as the optimization algorithm.

**RLCS specifics**: Dynamically adjusts data difficulty using curriculum sampling — starting with easier problems and progressively increasing difficulty. Uses dynamic sampling expansion with ratio EMA, larger batch sizes, and discards KL/entropy loss terms for stability.

**Critical finding on reward quality**: Even high-quality STEM verifiers cannot compensate for a flawed verifier in another domain (e.g., multi-image QA). One bad verifier causes reward hacking in its domain and performance collapse across ALL domains, including unrelated ones.

## Results
Evaluated across 42 public benchmarks in 8 categories:
- **GLM-4.5V**: SOTA among open-source models on General VQA (MMBench 88.2), STEM (MMMU 73.2, MathVista 79.2), OCR/Doc (DocVQA 97.0), GUI Agents (OSWorld 27.2), Coding (Design2Code 93.3)
- **GLM-4.1V-9B-Thinking**: Beats Qwen2.5-VL-72B on 29/28 benchmarks despite being ~8× smaller. Sets new SOTA among <10B models on 23/28 benchmarks
- **Cross-domain generalization**: RL training in one domain (e.g., STEM) genuinely improves performance in others (e.g., GUI agents) — positive transfer rather than interference

## Models Released
- **GLM-4.1V-9B-Thinking** — 9B VLM with thinking mode, Apache 2.0
- **GLM-4.5V** — 106B (12B active) MoE VLM, Apache 2.0
- **GLM-4.6V** — with native tool use and 128K context

## Connections
- Builds on: [[sources/deepseek-r1|DeepSeek-R1]] (GRPO algorithm), [[sources/idefics2|Idefics2]] (VLM design), [[sources/qwen25-vl|Qwen2.5-VL]]
- Competes with: [[sources/qwen25-vl|Qwen2.5-VL-72B]], [[sources/internvl-2-5|InternVL 2.5]], [[sources/cambrian|Cambrian-1]]
- Related concepts: [[concepts/vision-language-models]], [[concepts/rlhf]], [[concepts/grpo]], [[concepts/chain-of-thought]]
- From same org: [[sources/glm-4-5|GLM-4.5]]

## Citation
> Hong et al., "GLM-4.1V-Thinking: Towards Versatile Multimodal Reasoning with Scalable Reinforcement Learning," arXiv:2507.01006, 2025.
