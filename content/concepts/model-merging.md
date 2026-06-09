---
type: concept
tags: [model-merging, efficiency, transfer-learning]
---

# Model Merging

> Combining multiple fine-tuned models into a single model that inherits all their capabilities — without any additional training. Enabled by TIES-Merging and DARE.

## Overview
Model merging is one of the most surprising capabilities of neural networks: you can take two models fine-tuned from the same base (e.g., one for math, one for code) and combine their weights to get a single model that does both — at zero additional compute. This works because fine-tuning creates sparse, low-rank changes to the base model weights ("delta parameters"), and these changes are largely non-overlapping across different tasks.

## How It Works

### Basic Approaches
| Method | How | Quality |
|---|---|---|
| **Simple averaging** | θ_merged = (θ_A + θ_B) / 2 | Baseline — often loses performance |
| **Task arithmetic** | θ_merged = θ_base + (δ_A + δ_B) | Better — adds task-specific changes |
| **[[sources/ties-merging\|TIES-Merging]]** | Trim → Elect sign → Merge aligned | Best — resolves interference |
| **[[sources/dare\|DARE]]** | Drop 90-99% of deltas + rescale | Preprocessing step — removes noise |
| **DARE + TIES** | DARE first, then TIES | Industry standard combo |

### Why It Works
Fine-tuning creates **sparse** changes: only 1-10% of parameter changes are meaningful. The rest is noise that causes interference during merging. By trimming noise (DARE) and resolving sign conflicts (TIES), the meaningful task-specific knowledge can be combined cleanly.

### The DARE + TIES Pipeline
```
Base model
  → Fine-tune for math → δ_math
  → Fine-tune for code → δ_code  
  → Fine-tune for chat → δ_chat

DARE: Drop 90% of each delta, rescale survivors
TIES: Resolve sign conflicts across remaining deltas
Merge: θ_final = θ_base + merged_delta
```

## Tools
- **mergekit** (HF community) — the standard model merging toolkit. Supports: linear, slerp, TIES, DARE, DARE_TIES, and more
- Thousands of merged models on HF Hub
- No GPU needed — merging is a CPU-only operation on model weights

## Key Papers
- [[sources/ties-merging|TIES-Merging]] (2023) — resolves interference via trim, elect, merge
- [[sources/dare|DARE]] (2023) — 90-99% delta pruning with rescaling
- Task Arithmetic (2022) — foundational: δ_A + δ_B concept

## See Also
- [[concepts/lora-peft|LoRA / PEFT]]
- [[concepts/fine-tuning|Fine-tuning]]
- [[concepts/distillation|Distillation]]
