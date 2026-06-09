---
type: comparison
tags: [open-models, synthesis]
---

# Comparison: Open Model Families (2023–2025)

> Side-by-side analysis of the major open-source LLM families competing for the open-weight crown.

## Model Family Overview

| Family | Org | Sizes | Training Data | License | Key Strength |
|---|---|---|---|---|---|
| [[entities/models/llama\|Llama]] | Meta | 1B–405B | 2–15T tokens | Custom (permissive) | Ecosystem, community adoption |
| [[entities/models/mistral\|Mistral/Mixtral]] | Mistral AI | 7B–176B | Undisclosed | Apache 2.0 | Efficiency, MoE |
| [[entities/models/gemma\|Gemma]] | Google | 1B–27B | Undisclosed | Custom | Safety, Gemini technology |
| [[entities/models/qwen\|Qwen3]] | Alibaba | 0.6B–235B | 30T+ tokens | Apache 2.0 | Reasoning, 119 languages, unified thinking |
| [[entities/models/smollm\|SmolLM2]] | Hugging Face | 135M–1.7B | ~11T tokens | Apache 2.0 | Small model quality, transparency |
| [[entities/models/deepseek\|DeepSeek]] | DeepSeek | 7B–671B | Undisclosed | MIT | Reasoning, RL innovation |
| [[entities/models/phi\|Phi]] | Microsoft | 1.3B–14B | Synthetic-heavy | Microsoft RL | Synthetic data, STEM reasoning |

## Architecture Comparison

| Feature | Llama 3 | Mistral 7B | Mixtral 8x7B | Gemma 2 | Qwen3-32B | Phi-4 |
|---|---|---|---|---|---|---|
| Attention | GQA | GQA | GQA | Interleaved local/global | GQA + QKV bias | GQA |
| Position Encoding | RoPE | RoPE | RoPE | RoPE | RoPE | RoPE |
| Activation | SwiGLU | SwiGLU | SwiGLU | GeGLU | SwiGLU | SwiGLU |
| Normalization | RMSNorm | RMSNorm | RMSNorm | RMSNorm | RMSNorm | RMSNorm |
| MoE | No | No | Yes (8 experts) | No | Optional (128 experts) | No |
| Context | 128K | 32K | 32K | 8K | 32K (ext 128K+) | 16K |
| Thinking Mode | No | No | No | No | **Yes** (think/no-think) | No |

**Note**: The "LLaMA architecture template" (RMSNorm + SwiGLU + RoPE + GQA) has become the de facto standard. Nearly all open models follow this pattern.

## Key Differentiators

### Meta (Llama)
- **Largest ecosystem** — most community fine-tunes, adapters, and tools
- Progressively more open licensing
- Most detailed alignment documentation (Llama 2)
- Llama 3.1-405B: largest open-weight model

### Mistral AI
- **Best efficiency** — Mistral 7B outperforms Llama 2 13B (2× smaller)
- Pioneered open-source MoE with Mixtral
- Fast iteration; minimalist papers

### Google (Gemma)
- **Safety emphasis** — most comprehensive responsible AI documentation
- Benefits from Gemini research infrastructure
- Strong at small scale (2B)

### Alibaba (Qwen)
- **Widest size range** — 0.6B to 235B, dense + MoE, covering all use cases
- **119 languages** — strongest multilingual support
- **Unified thinking mode** — single deployment for both chat and reasoning
- Qwen3-30B-A3B (3B active) matches DeepSeek-R1 (671B total) on reasoning
- Most upvoted model paper on HF Papers (339 upvotes)

### Hugging Face (SmolLM)
- **Most transparent** — detailed ablations on data mixing
- Focused on making small models capable
- Open training recipes and datasets

### DeepSeek
- **Reasoning frontier** — DeepSeek-R1 matches OpenAI o1
- Invented GRPO; pioneered pure-RL training
- Most innovative MoE architecture (MLA + fine-grained experts)

### Microsoft (Phi)
- **Synthetic data pioneer** — proved data quality > parameter count
- Phi-4 (14B) beats GPT-4o on GPQA and MATH
- Edge deployment focus (Phi-3-mini on phones)
- 50+ synthetic dataset types for pretraining

## The Arc of Progress (7B-class models)
| Model | Date | Key Benchmark | Notable |
|---|---|---|---|
| Llama 2 7B Chat | Jul 2023 | ~6.3 MT-Bench | First open RLHF chat |
| Mistral 7B Instruct | Oct 2023 | ~6.8 MT-Bench | Outperformed Llama 2 13B |
| Zephyr 7B | Oct 2023 | ~7.3 MT-Bench | AI feedback, no human annotation |
| Gemma 7B IT | Mar 2024 | ~7.0 MT-Bench | Gemini technology |
| Qwen2.5-7B Instruct | Dec 2024 | 128K context | 18T tokens, multilingual |
| Qwen3-8B | May 2025 | Thinking mode | Unified reasoning + chat |

## The Reasoning Race (Latest)
| Model | Active Params | AIME 2024/2025 | MATH-500 | Open? |
|---|---|---|---|---|
| Qwen3-235B-A22B | 22B | 81.5 (2025) | 98.2 | ✅ Apache 2.0 |
| DeepSeek-R1 | ~37B (of 671B) | 79.8 | 97.3 | ✅ MIT |
| Phi-4 | 14B | — | 80.4 | ✅ MS License |
| Qwen3-30B-A3B | 3B | — | 95.2 | ✅ Apache 2.0 |

## See Also
- [[comparisons/alignment-methods]]
- [[comparisons/reasoning-models]]
- [[comparisons/pretraining-data]]
- [[concepts/transformer-architecture]]
- [[concepts/scaling-laws]]
