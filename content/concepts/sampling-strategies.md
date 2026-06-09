---
type: concept
tags: [inference, decoding, generation, temperature]
---

# Sampling Strategies (Decoding Methods)

> The algorithms that determine **how tokens are selected** during LLM generation — from deterministic greedy decoding to stochastic sampling with temperature, top-k, and top-p.

## Methods

### Deterministic
| Method | How | Use Case |
|---|---|---|
| **Greedy** | Highest-probability token | Code, factual QA |
| **Beam Search** | Track top-k sequences | Translation, summarization |

### Stochastic
| Method | How | Use Case |
|---|---|---|
| **Temperature** | Scale logits by `1/T` | T<1: focused; T>1: diverse |
| **Top-k** | Sample from top k tokens | General generation |
| **Top-p (Nucleus)** | Smallest set with cumulative prob ≥ p | Adaptive vocabulary |
| **Min-p** | Remove tokens < `p × max_prob` | Cleaner than top-p |

## Temperature Guide
| Temperature | Effect | Best For |
|---|---|---|
| T = 0 | Greedy (deterministic) | Factual, code |
| T = 0.3–0.7 | Focused but varied | Chat, instructions |
| T = 0.8–1.0 | Balanced | Creative writing |

## Sampling for Reasoning
- **[[sources/deepseek-r1\|DeepSeek-R1]]**: Temperature 0.6–1.0 during RL for exploration
- **[[sources/qwen3\|Qwen3]] thinking**: Temperature 0.6 recommended
- **Self-consistency** ([[concepts/chain-of-thought\|CoT]]): Sample N chains, majority vote
- **Best-of-N**: Sample N, select via [[concepts/reward-modeling\|reward model]]

## Special Strategies
- **[[concepts/structured-generation\|Constrained decoding]]**: Mask invalid tokens for JSON/regex
- **Budget forcing** ([[sources/s1\|s1]]): Suppress end-of-thinking token to extend reasoning
- **Repetition penalties**: Prevent degenerate loops

## See Also
- [[concepts/structured-generation]] — Grammar-constrained decoding
- [[concepts/speculative-decoding]] — Parallel token generation
- [[concepts/chain-of-thought]] — Self-consistency uses sampling
- [[concepts/test-time-compute]] — Best-of-N and self-consistency