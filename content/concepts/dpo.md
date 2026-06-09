---
type: concept
tags: [alignment, dpo]
---

# DPO (Direct Preference Optimization)

> A **simplified alignment method** that eliminates the need for a separate reward model and RL loop — directly optimizing the policy on preference pairs using a classification loss.

## Overview
DPO, introduced in [[sources/dpo|Rafailov et al. 2023]], showed that the RLHF objective has a closed-form solution. Instead of training a reward model and then doing PPO, you can directly optimize the language model on (chosen, rejected) pairs with a simple binary cross-entropy loss. This made alignment dramatically simpler, more stable, and more accessible.

## How It Works

### The DPO Loss
```
L_DPO = -E[log σ(β · (log π_θ(y_w|x)/π_ref(y_w|x) - log π_θ(y_l|x)/π_ref(y_l|x)))]
```

Where:
- `y_w` = preferred (winning) response
- `y_l` = dispreferred (losing) response
- `π_θ` = policy being trained
- `π_ref` = frozen reference model (usually the SFT model)
- `β` = temperature controlling deviation from reference

**Intuition**: Increase the probability of preferred responses relative to the reference, and decrease the probability of dispreferred responses. The log-ratio margin between chosen and rejected should increase.

### What You Need
- A trained SFT model (serves as π_ref and initialization)
- A dataset of (prompt, chosen_response, rejected_response) triples
- Standard supervised training infrastructure — no RL libraries needed

### Advantages Over PPO-based RLHF
| Aspect | RLHF (PPO) | DPO |
|---|---|---|
| Reward model | Required (separate model) | Not needed |
| RL infrastructure | Required (PPO, value head, etc.) | Not needed |
| Training stability | Sensitive to hyperparameters | More stable |
| Memory | 4 models in memory | 2 models |
| Compute | Expensive (sampling + RL) | Cheap (supervised) |

## Variants & Extensions
| Variant | Innovation |
|---|---|
| **IPO** | Uses squared hinge loss instead of sigmoid; no β sensitivity |
| **KTO** | Works with binary feedback (good/bad) — no paired data needed |
| **ORPO** | Combines SFT and DPO into a single loss — no reference model |
| **SimPO** | Uses average log-probability as reward — no reference model |
| **CPO** | Contrastive preference optimization |
| **dDPO** | Distilled DPO — AI-generated preferences ([[sources/zephyr]]) |

## Key Papers
- [[sources/dpo]] — Original DPO paper
- [[sources/zephyr]] — Applied dDPO for chat alignment
- [[sources/mixtral]] — Mixtral Instruct uses DPO

## See Also
- [[concepts/rlhf]]
- [[concepts/grpo]]
- [[concepts/instruction-tuning]]
