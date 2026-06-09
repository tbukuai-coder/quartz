---
type: concept
tags: [alignment, preference-optimization, dpo, kto, orpo]
---

# Preference Optimization — Beyond DPO

> The family of algorithms that align LLMs with human preferences — from paired preferences (DPO) to binary labels (KTO) to reference-free monolithic training (ORPO). All natively supported in TRL.

## Overview
After DPO simplified RLHF in 2023, a wave of follow-up methods addressed its remaining limitations: the need for paired preference data, the reference model memory overhead, and the two-stage SFT→DPO pipeline. Each method in the family trades different constraints for different advantages.

## The Alignment Family

| Method | Data Format | Ref Model? | Stages | Key Advantage |
|---|---|---|---|---|
| **[[concepts/rlhf\|RLHF/PPO]]** | Reward model | ✅ (reward + ref) | 3 (SFT→RM→RL) | Most flexible, highest ceiling |
| **[[concepts/dpo\|DPO]]** | Paired (chosen, rejected) | ✅ | 2 (SFT→DPO) | Simple, no reward model |
| **[[sources/kto\|KTO]]** | Binary (good/bad) | ✅ | 2 (SFT→KTO) | Cheapest data (no pairs needed) |
| **[[sources/orpo\|ORPO]]** | Paired (chosen, rejected) | ❌ | **1** | Fewest stages, lowest compute |
| **[[concepts/grpo\|GRPO]]** | Rule-based rewards | ❌ critic | 1-2 | Best for verifiable tasks (math) |

## Key Innovations

### KTO — Binary Signal Alignment ([[sources/kto]])
- Only needs "good" or "bad" labels per output — no need to construct pairs
- Grounded in Kahneman-Tversky prospect theory (loss aversion)
- Matches DPO with simpler data collection
- `trl.KTOTrainer`

### ORPO — Monolithic Optimization ([[sources/orpo]])
- Merges SFT and preference alignment into one loss function
- No reference model — halves GPU memory
- Half the compute of SFT+DPO pipeline
- `trl.ORPOTrainer`

## When to Use What

```
"I have paired preference data and compute"      → DPO
"I only have thumbs up/down labels"              → KTO
"I want the simplest pipeline possible"          → ORPO
"I have verifiable correct answers (math/code)"  → GRPO
"I need maximum quality on complex tasks"        → RLHF/PPO
```

## Key Papers
- [[sources/dpo|DPO]] (2023) — Direct Preference Optimization
- [[sources/kto|KTO]] (2024) — Kahneman-Tversky Optimization
- [[sources/orpo|ORPO]] (2024) — Odds Ratio Preference Optimization
- [[sources/deepseekmath|GRPO]] (2024) — Group Relative Policy Optimization
- [[sources/instructgpt|InstructGPT/RLHF]] (2022) — Original RLHF pipeline

## See Also
- [[concepts/rlhf|RLHF]]
- [[concepts/dpo|DPO]]
- [[concepts/grpo|GRPO]]
- [[comparisons/alignment-methods|Alignment Methods Comparison]]
