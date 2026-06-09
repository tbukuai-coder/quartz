---
type: entity
category: model
tags: [architecture, hybrid, ssm, moe, long-context, ai21-labs]
---

# Jamba

> AI21 Labs' **hybrid Transformer-Mamba-MoE** model family — the first production-scale architecture combining attention, state space models, and sparse experts, fitting 52B parameters on a single 80GB GPU with 256K context.

## Overview
Jamba challenged the assumption that the Transformer is the only viable architecture for large language models. By interleaving Mamba SSM layers with occasional attention layers and MoE routing, Jamba achieves superior throughput and memory efficiency — particularly for long sequences.

## Model Family
| Model | Total Params | Active Params | Context | Year |
|---|---|---|---|---|
| Jamba-v0.1 | 52B | 12B | 256K | 2024 |
| Jamba-1.5-Mini | 12B | — | 256K | 2024 |
| Jamba-1.5-Large | 98B | — | 256K | 2024 |

## Architecture
- **Ratio**: 1:7 attention-to-Mamba layers (optimal from ablations)
- **MoE**: 16 experts, top-2 routing on alternating layers
- **Memory**: SSM layers have constant-size state (no [[concepts/kv-cache|KV cache]] growth)

### Memory Advantage at 256K Context
| Model | KV Cache | Fits On |
|---|---|---|
| Jamba (52B) | ~12 GB | 1× 80GB GPU |
| Mixtral (47B) | ~200+ GB | Multi-GPU |

## Related Papers
- [[sources/jamba]] — Jamba: A Hybrid Transformer-Mamba Language Model

## See Also
- [[entities/orgs/ai21-labs]] — AI21 Labs (creator)
- [[concepts/state-space-models]] — Mamba SSM component
- [[concepts/mixture-of-experts]] — MoE component
- [[concepts/kv-cache]] — Jamba's key memory advantage