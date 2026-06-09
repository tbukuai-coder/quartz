---
type: source
arxiv_id: "2411.15124"
title: "Tülu 3: Pushing Frontiers in Open Language Model Post-Training"
authors: ["Nathan Lambert", "Jacob Morrison", "Valentina Pyatkin", "et al."]
date: 2024-11-22
org: "AllenAI"
tags: [alignment, sft, dpo, rlvr, open-science, 2024]
upvotes: 67
---

# Tülu 3

> The **definitive open post-training recipe** — a fully transparent pipeline of SFT → DPO → RLVR (Reinforcement Learning with Verifiable Rewards) that surpasses Llama 3.1 Instruct, Qwen 2.5 Instruct, and even closed models like GPT-4o-mini and Claude 3.5-Haiku. All data, code, and training recipes released.

## Key Contributions
- **Complete open post-training recipe**: First fully documented, reproducible pipeline surpassing proprietary instruct models
- **RLVR (Reinforcement Learning with Verifiable Rewards)**: Novel method using verifiable answers (math, code) as rewards for RL, applied after DPO
- **Multi-task evaluation framework**: Development and unseen evaluation splits with standard benchmark implementations
- **Substantial decontamination**: Rigorous removal of benchmark data from open training datasets
- **Negative results documented**: Transparent reporting of methods that didn't reliably improve performance

## Method — Three-Stage Pipeline

### Stage 1: Supervised Fine-Tuning (SFT)
- Diverse, skill-centric instruction data covering math, code, safety, general chat, instruction following
- Careful data curation with quality filtering
- Trains the model to follow instructions in the target format

### Stage 2: Direct Preference Optimization (DPO)
- On-policy preference data: generate completions from the SFT model, then rank using reward models
- Significantly outperforms off-policy preference data (pre-generated completions)
- Uses diverse prompt sources for broad skill coverage

### Stage 3: RLVR (Reinforcement Learning with Verifiable Rewards)
- Novel contribution: RL stage using problems with verifiable answers (math, code execution)
- Reward = 1 if the model's answer matches the ground truth, 0 otherwise
- Applied using PPO-style optimization after DPO
- Key insight: RLVR provides complementary signal to DPO — further improves reasoning without degrading other skills

## Results
| Model | IFEval | GSM8K | MATH | AlpacaEval |
|---|---|---|---|---|
| Tülu 3 70B | **Strong** | **Strong** | **Strong** | **Strong** |
| Llama 3.1 70B Instruct | Below Tülu 3 | Below Tülu 3 | Below Tülu 3 | Below Tülu 3 |
| Qwen 2.5 72B Instruct | Competitive | Competitive | Competitive | Below Tülu 3 |
| GPT-4o-mini | Below Tülu 3 | Below Tülu 3 | — | — |

Tülu 3 builds on Llama 3.1 base models and surpasses their official instruct versions.

## What Didn't Work (Documented Negative Results)
- Some data augmentation strategies hurt performance
- Certain RL configurations destabilized training
- Some evaluation metrics didn't correlate with real-world quality
- Transparent documentation of failures is a key contribution for the community

## Impact
- **[[sources/olmo|OLMo 2]]** uses the Tülu 3 recipe for post-training (SFT + DPO + RLVR)
- Established RLVR as a standard post-training technique alongside SFT and DPO
- Tülu datasets widely used for alignment research
- Influenced the shift toward verifiable reward signals in open-source alignment

## Datasets
- [[entities/datasets/tulu|Tülu]] — alignment datasets (SFT + DPO)
- Uses permissively licensed data sources

## Connections
- Builds on: [[sources/dpo|DPO]], [[sources/llama-3|Llama 3.1]] (base models)
- Extended by: OLMo 2 post-training
- Related: [[concepts/rlhf|RLHF]], [[concepts/dpo|DPO]], [[concepts/grpo|GRPO]]
- Org: [[entities/orgs/allenai|AllenAI]]

## Citation
> Lambert et al., "Tülu 3: Pushing Frontiers in Open Language Model Post-Training," arXiv:2411.15124, 2024.
