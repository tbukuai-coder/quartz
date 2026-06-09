---
type: entity
category: org
tags: [zhipu-ai, reasoning, multimodal, agents, moe]
---

# Zhipu AI

> The creator of the **GLM** model family — building comprehensive open-source models spanning text (GLM-4.5), multimodal reasoning (GLM-4.1V-Thinking), and agentic AI, with state-of-the-art results on coding, GUI agents, and scientific reasoning.

## Overview
Zhipu AI (智谱AI) is a Chinese AI research company that has rapidly emerged as a major force in open-source AI through its GLM model family. Their approach emphasizes both reasoning and agentic capabilities, with a unique focus on training-time RL across all multimodal domains simultaneously.

## Key Contributions

### Models
- **[[sources/glm-4-5|GLM-4.5]]** (2025): 355B (32B active) MoE — ranks 3rd overall, 2nd on agentic benchmarks. Expert Model Iteration post-training. Uses Muon optimizer.
- **[[sources/glm-4.1v-thinking|GLM-4.1V-Thinking]]** (2025): 9B VLM that beats Qwen2.5-VL-72B on 29 benchmarks. Introduces RLCS (Reinforcement Learning with Curriculum Sampling).
- **GLM-4.5V** (2025): 106B (12B active) MoE VLM — SOTA among open-source VLMs on nearly all tasks.
- **GLM-4.6V** (2025): Open-source multimodal with native tool use and 128K context.

### Key Innovations
- **RLCS (RL with Curriculum Sampling)**: Multi-domain RL framework that progressively increases difficulty. Critical finding: one bad reward verifier collapses training across ALL domains.
- **Expert Model Iteration**: Train specialized expert models (reasoning, agent, general chat) independently, then unify via self-distillation.
- **Deeper-is-better MoE**: GLM-4.5 uses 89 MoE layers (vs. DeepSeek-V3's 58), finding that depth > width for reasoning.
- **Slime RL Infrastructure**: High-performance RL system using Megatron + SGLang.

## Papers in This Wiki
- [[sources/glm-4-5]] — GLM-4.5: ARC Foundation Models
- [[sources/glm-4.1v-thinking]] — GLM-4.1V-Thinking: Multimodal Reasoning

## See Also
- [[entities/orgs/deepseek]] — DeepSeek (competing Chinese AI lab)
- [[entities/orgs/alibaba]] — Alibaba / Qwen (competing model family)
- [[concepts/mixture-of-experts]] — MoE architecture
- [[concepts/vision-language-models]] — VLM design
- [[concepts/grpo]] — GRPO (used in GLM RL)
