---
type: source
arxiv_id: "2605.06130"
title: "Skill1: Unified Evolution of Skill-Augmented Agents via Reinforcement Learning"
authors:
  - Yaorui Shi
  - Yuxin Chen
  - Zhengxi Lu
  - Yuchun Miao
  - Shugui Liu
  - Qi GU
  - Xunliang Cai
  - Xiang Wang
  - An Zhang
venue: arXiv
year: 2026
month: 5
date: "2026-05"
upvotes: 28
tags:
  - agents
  - reinforcement-learning
  - skill-library
  - credit-assignment
  - alfworld
  - webshop
---

# Skill1: Unified Evolution of Skill-Augmented Agents via Reinforcement Learning

## One-Line Summary

Single-policy RL framework that jointly optimizes skill selection, utilization, and distillation through shared task-outcome credit assignment, achieving 97.5% success on ALFWorld by co-evolving all three capabilities simultaneously.

## Key Contributions

1. **Unified skill lifecycle optimization** — First framework to train a single policy across all three stages of the skill-augmented agent loop: selection → utilization → distillation.
2. **Shared task-outcome signal with decomposition** — All learning signals derived from one task outcome $r(\tau)$, decomposed into:
   - **Utilization credit**: $R_i^{\text{util}} = r(\tau_i)$ — direct task outcome
   - **Selection credit**: NDCG-based re-ranking reward against per-skill utility trends (EMA of outcomes)
   - **Distillation credit**: $R_i^{\text{distill}} = r(\tau_i) - \hat{U}_i$ — variation above library's best trend (is this experience better than what we already know?)
3. **Co-evolution dynamics** — Demonstrates mutual reinforcement: selection precision converges first (step 20), accelerating utilization and distillation (step 60). Removing any credit signal degrades all three capabilities.
4. **SOTA on skill-augmented agents** — 97.5% average success on ALFWorld (+2.6 over RetroAgent), 82.9% on WebShop.

## Method

### Agent Workflow

For each task $x \sim \mathcal{D}$:

**1. Skill Selection**
- Generate natural-language query $q \sim \pi_\theta(\cdot|x)$
- Frozen encoder $\mathcal{E}$ (all-MiniLM-L6-v2) retrieves top-K candidates by semantic similarity
- Policy re-ranks candidates via permutation $\sigma \sim \pi_\theta(\cdot|x, \mathcal{B}_K)$
- Top-ranked skill $z$ selected for utilization

**2. Skill Utilization**
- Multi-turn interaction with environment: $\tau \sim \pi_\theta(\cdot|x, z.\text{strat}, o_{\leq t})$
- Up to $T$ turns, terminal reward $r(\tau) \in \{0,1\}$

**3. Skill Distillation**
- Policy reflects on trajectory to produce:
  - $s_{\text{new}}.\text{strat}$: reusable strategy summary
  - $s_{\text{new}}.\text{desc}$: scenario description for when skill applies
- Admitted to library $\mathcal{B}$ only when $r(\tau) = 1$
- Library capacity $|\mathcal{B}| \leq 5000$; retirement heuristic: $U(s) \cdot \log(n(s))$ removes low-utility, infrequently-used skills

### Reward Assignment

**Utilization**: Direct outcome $R_i^{\text{util}} = r(\tau_i)$

**Selection**: Two mechanisms:
1. Query generation receives gradients through utilization objective (better queries → better candidates → higher $r(\tau)$)
2. Re-ranking reward via NDCG against skill utility trends:
   $$U(s) \leftarrow (1-\alpha) \cdot U(s) + \alpha \cdot r(\tau_i), \quad \forall s \in \mathcal{B}_K$$
   $$R_i^{\text{rerank}} = \text{NDCG}(\sigma_i, \text{argsort}(-U(\mathcal{B}_K^i)))$$

**Distillation**: Variation above library's best trend:
$$R_i^{\text{distill}} = r(\tau_i) - \hat{U}_i, \quad \hat{U}_i = \max_{s \in \mathcal{B}_K^i} U(s)$$
Positive = experience surpasses current library → distill. Negative = redundant → discourage.

### Joint Optimization

All three rewards combined with weights $\lambda_1$ (selection), $\lambda_2$ (distillation):
$$\mathcal{L} = \mathcal{L}_{\text{GRPO}}^{\text{util}} + \lambda_1 \mathcal{L}_{\text{GRPO}}^{\text{rerank}} + \lambda_2 \mathcal{L}_{\text{GRPO}}^{\text{distill}}$$

## Results

### ALFWorld (Success Rate %)

| Method | Pick | Look | Clean | Heat | Cool | Pick2 | Avg |
|---|---|---|---|---|---|---|---|
| ReAct | 48.5 | 35.4 | 34.3 | 13.2 | 18.2 | 17.6 | 31.2 |
| GRPO | 90.8 | 66.1 | 89.3 | 74.7 | 72.5 | 64.7 | 77.6 |
| RetroAgent | 97.9 | 90.9 | 99.2 | 92.9 | 85.3 | 91.0 | 94.9 |
| **Skill1** | **100.0** | **98.6** | 97.3 | **99.2** | **96.1** | **96.0** | **97.5** |

### WebShop
- Skill1: **82.9%** success
- Best prior (RetroAgent): **82.3%**

### Ablations (ALFWorld)
- w/o Selection: -5.7 points (concentrated on multi-step tasks)
- w/o Distillation: -5.1 points
- w/o Library entirely: -16.6 points (largest drop — Heat/Pick2 lose 28+ points)
- $\lambda_1 = 0$: -3.5 points
- $\lambda_2 = 0$: -2.6 points
- $\lambda_1 = \lambda_2 = 0$: -7.3 points (worse than removing each individually — signals are complementary)

## Connections

- **Skill Evolution Narrative**: Unifies the skill-augmented agent space with [[sources/skill-text-to-skill-structure|SSL Skills]] (structured disentanglement), [[sources/skillos|SkillOS]] (streaming skill curation), and [[sources/web2bigtable|Web2BigTable]] (internet-scale skill extraction). Where SSL provides representation and SkillOS provides curation, Skill1 provides the *training framework* for unified evolution.
- **Credit Assignment**: Low-frequency/high-frequency decomposition of task outcome parallels [[sources/lenvm|LenVM]]'s token-level value estimation and [[sources/repro|RePro]]'s process reward lens — all decompose sparse terminal signals into dense training gradients.
- **GRPO Foundation**: Built on [[concepts/grpo|GRPO]] with group-based advantage estimation, extending [[sources/agentic-rl-reasoning|Agentic RL]] and [[sources/multi-turn-agent-rl|Multi-Turn Agent RL]] to the skill library lifecycle.
- **Memory Systems**: Per-skill EMA utility trends share design philosophy with [[sources/mia-signature|MiA-Signature]]'s global activation tracking — both maintain evolving quality estimates over distributed memory.
- **Benchmark**: ALFWorld and WebShop are standard agent evaluation environments also used by [[sources/eywa|Eywa]] and [[sources/agentic-rl-reasoning|Agentic RL]] for cross-domain validation.

## Citation

```bibtex
@article{shi2026skill1,
  title={Skill1: Unified Evolution of Skill-Augmented Agents via Reinforcement Learning},
  author={Shi, Yaorui and Chen, Yuxin and Lu, Zhengxi and Miao, Yuchun and Liu, Shugui and GU, Qi and Cai, Xunliang and Wang, Xiang and Zhang, An},
  journal={arXiv preprint arXiv:2605.06130},
  year={2026}
}
```

---
*Ingested in Batch 26 (2026-05-05)* | [[index]] | [[concepts/agents]] | [[concepts/grpo]] | [[comparisons/rl-reasoning-methods]]