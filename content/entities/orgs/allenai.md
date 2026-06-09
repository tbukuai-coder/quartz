---
type: entity
category: org
tags: [allenai, open-science, pre-training, nlp, research]
---

# AllenAI (Allen Institute for AI)

> A non-profit AI research institute founded by Paul Allen — pioneering the **open-science** approach to LLM development with fully open models (OLMo), datasets (Dolma), and training infrastructure.

## Overview
AllenAI (AI2) is the leading advocate for fully open AI research. While other organizations release "open-weight" models (LLaMA, Mistral) that withhold training data and code, AllenAI releases **everything**: model weights, training data, training code, evaluation code, intermediate checkpoints, and training logs. This philosophy enables true scientific reproducibility and has spawned an ecosystem of research building on their artifacts.

## Key Contributions

### Open Language Models
- [[entities/models/olmo|OLMo]] — First truly open LLM: weights + data + code + logs (1B, 7B)
- [[sources/olmoe|OLMoE]] — Fully open sparse MoE (1B active / 7B total, 5T tokens, outperforms Llama2-13B-Chat)
- OLMo 2 — Improved stability + RLVR (Reinforcement Learning with Verifiable Rewards)
- **[[sources/olmo-3|OLMo 3]]** — SOTA fully-open models at 7B/32B; **OLMo 3 Think 32B** is the strongest fully-open thinking model, targeting reasoning, function calling, coding, and general chat

### Open Datasets
- [[entities/datasets/dolma|Dolma]] — 3T token open pretraining corpus with documented curation
- OLMoE-Mix — 5T token MoE training mixture (DCLM + Dolma + StarCoder + peS2o)
- DCLM (DataComp for Language Models) — Data curation benchmark using OLMo

### Adaptation & Alignment
- **Tülu** — Adaptation recipes (SFT + DPO) for OLMo family
- **Tülu 3** — Updated SFT dataset used by OLMoE-Instruct

### Research Infrastructure
- Trained on both NVIDIA (A100) and AMD (MI250X on LUMI supercomputer) GPUs
- All W&B training logs publicly available
- Intermediate checkpoints released for reproducibility research

## Open-Science Philosophy
AllenAI's releases set a new standard for open-source AI:

| Artifact | AllenAI (OLMo) | Meta (LLaMA) | Mistral | DeepSeek |
|---|---|---|---|---|
| Model weights | ✅ | ✅ | ✅ | ✅ |
| Training data | ✅ (Dolma) | ❌ | ❌ | ❌ |
| Training code | ✅ | ❌ | ❌ | ✅ |
| Training logs | ✅ (W&B) | ❌ | ❌ | ❌ |
| Eval framework | ✅ (Paloma) | ❌ | ❌ | ❌ |
| Checkpoints | ✅ (all) | ❌ | ❌ | ❌ |

## Other Notable Projects
- **Semantic Scholar** — AI-powered academic search (hosts peS2o corpus)
- **Paloma** — Perplexity-based evaluation benchmark for LMs
- **AI2 PRIOR** — Computer vision and robotics research

## Papers in This Wiki
- [[sources/olmo]] — OLMo: Accelerating the Science of Language Models
- [[sources/olmo-2]] — OLMo 2: Improved training recipe
- [[sources/olmo-3]] — OLMo 3: SOTA fully-open thinking model (7B, 32B)
- [[sources/olmoe]] — OLMoE: Open Mixture-of-Experts Language Models

## See Also
- [[entities/models/olmo]]
- [[entities/datasets/dolma]]
- [[concepts/pre-training]]
- [[concepts/mixture-of-experts]]
- [[concepts/training-infrastructure]]
