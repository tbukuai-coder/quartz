---
type: entity
category: org
tags: [apple, open-science, small-model, on-device, 2024]
---

# Apple

> Consumer technology giant that entered the open LLM space in 2024 with OpenELM, emphasizing on-device inference and full open-science releases.

## Overview
Apple joined the open-source LLM movement with [[sources/openelm|OpenELM]] (2024), releasing not just weights but training code, logs, checkpoints, and data recipes — matching the open-science standard set by [[entities/orgs/allenai|AllenAI]]. Apple's focus is on **efficient, on-device models** that run on Apple Silicon via the MLX framework.

## Key Contributions
- **OpenELM** (2024): Family of efficient models (270M–3B) with layer-wise scaling, open training framework
- **MLX framework**: Hardware-optimized inference on Apple Silicon
- **Layer-wise scaling**: Innovation that varies parameter allocation across Transformer layers
- **On-device focus**: Models designed for mobile and edge deployment

## Related Papers
- [[sources/openelm|OpenELM]] — Layer-wise scaling, open training

## See Also
- [[entities/orgs/microsoft|Microsoft]] — Phi series (another on-device focused org)
- [[entities/orgs/huggingface|Hugging Face]] — SmolLM (small model focus)
- [[comparisons/small-language-models|Small Language Models]] comparison
