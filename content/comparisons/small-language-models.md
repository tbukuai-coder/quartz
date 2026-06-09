---
type: comparison
tags: [small-models, efficiency, data-centric, synthesis]
---

# Comparison: Small Language Models (<3B Parameters)

> Proving that data quality and training methodology matter more than parameter count.

## Model Comparison

| Model | Params | Tokens | Ratio | Key Data | Highlight |
|---|---|---|---|---|---|
| [[entities/models/smollm\|SmolLM2-1.7B]] | 1.7B | ~11T | 6,500:1 | FineWeb-Edu, [[entities/datasets/cosmopedia\|Cosmopedia]] | Best-in-class <2B |
| [[entities/models/phi\|Phi-3-mini]] | 3.8B | 4.9T | 1,300:1 | Synthetic textbooks + web | Strong STEM |
| [[entities/models/qwen\|Qwen3-0.6B]] | 0.6B | 36T+ | 60,000:1 | Massive diverse mix | Thinking mode at 0.6B |
| [[entities/models/qwen\|Qwen3-1.7B]] | 1.7B | 36T+ | 21,000:1 | Massive diverse mix | 119 languages |
| [[entities/models/gemma\|Gemma-2-2B]] | 2.6B | ~2T | 770:1 | Gemini infrastructure | Strong safety |
| [[entities/models/llama\|Llama-3.2-1B]] | 1.2B | ~15T | 12,500:1 | Llama mix | Ecosystem compat |
| [[entities/models/smollm\|SmolLM2-135M]] | 135M | ~11T | 81,000:1 | FineWeb-Edu | Ultra-tiny, edge |

## Key Strategies
1. **Overtraining**: Far beyond Chinchilla-optimal (20:1) — small models benefit from 1,000–60,000:1
2. **Data quality**: Curated > unfiltered. [[sources/phi-4|Phi-4]] synthetic beats 70B; FineWeb-Edu beats raw web
3. **Multi-stage training**: Web → high-quality → SFT → DPO
4. **Distillation**: [[sources/deepseek-r1|R1]]-Distill, [[sources/smolvlm|SmolVLM]]

## Deployment

| Use Case | Model | Why |
|---|---|---|
| Mobile/Edge | SmolLM2-135M/360M | Ultra-small |
| On-device assistant | SmolLM2-1.7B / Qwen3-1.7B | Best <2B |
| Embedded reasoning | Qwen3-0.6B (thinking) | CoT at 0.6B |
| Vision on device | SmolVLM-256M | <1GB, beats 80B predecessors |

## See Also
- [[entities/models/smollm]] — SmolLM2
- [[entities/models/phi]] — Phi series
- [[concepts/scaling-laws]] — Overtraining vs Chinchilla
- [[concepts/distillation]] — Knowledge distillation
- [[comparisons/open-model-families]] — Full model comparison