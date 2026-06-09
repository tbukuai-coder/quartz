---
type: source
arxiv_id: "2605.06507"
title: "MARBLE: Multi-Aspect Reward Balance for Diffusion RL"
authors:
  - Canyu Zhao
  - Hao Chen
  - Yunze Tong
  - Yu Qiao
  - Jiacheng Li
  - Chunhua Shen
venue: arXiv
year: 2026
month: 5
date: "2026-05"
upvotes: 32
tags:
  - diffusion-models
  - reinforcement-learning
  - multi-objective-optimization
  - gradient-harmonization
  - image-generation
github: https://github.com/aim-uofa/MARBLE
stars: 23
---

# MARBLE: Multi-Aspect Reward Balance for Diffusion RL

## One-Line Summary

Gradient-space optimization framework that harmonizes multiple reward signals for diffusion model RL fine-tuning via per-reward advantage decomposition, normalized gradient QP solving, and amortized coefficient smoothing — achieving simultaneous improvement on all rewards with a single model.

## Key Contributions

1. **Characterizes specialist sample problem** — In multi-reward diffusion RL, 80% of mini-batches show anti-aligned weighted-sum gradients (update actively pushes against at least one reward). Formally quantifies why scalar reward aggregation fails.
2. **MARBLE framework** — Three components:
   - **Per-reward advantage decomposition**: Independent advantage estimator per reward so each sample is credited only on informative dimensions
   - **Normalize-and-rescale gradient harmonization**: Solves convex QP on unit-normalized gradients to find common descent direction improving all rewards
   - **Amortized formulation**: Exploits affine structure of DiffusionNFT loss to reduce multi-reward training cost to near single-reward baseline
3. **EMA coefficient smoothing**: Stabilizes amortized balancing weights against transient single-batch fluctuations, preventing rewards from being transiently silenced.
4. **First multi-reward diffusion RL solution** — Prior art required either separate models per reward, hand-crafted sequential schedules, or suffered from scalar aggregation failures.

## Method

### Specialist Sample Problem

In diffusion RL with multiple rewards $\{R_k\}_{k=1}^K$, most rollouts are informative for only a subset of rewards:
- Cat image → strong aesthetic signal, no OCR signal
- Text rendering → strong OCR signal, average aesthetics

Weighted sum $R(x) = \sum_k w_k R_k(x)$ dilutes informative dimensions. Gradient-level diagnosis: weighted-sum update is anti-aligned with at least one reward's gradient in **80% of mini-batches**.

### MARBLE Algorithm

**Step 1: Per-reward advantage decomposition**
$$A_k(x) = \frac{R_k(x) - \mu_k(\text{prompt})}{\sigma_k(\text{prompt}) + \varepsilon}$$
Each $A_k$ yields separate interpolation coefficient $r_k \in [0,1]$ and reward-specific NFT loss $\ell_k$.

**Step 2: Gradient computation**
$$g_k = \nabla_\theta \frac{1}{NT}\sum_{i=1}^N \sum_{t=1}^T \ell_k(\theta; x_i, t)$$
K backward passes on same batch; only advantage signal differs.

**Step 3: Normalization**
$$\hat{g}_k = g_k / \|g_k\|$$
Removes scale disparities between rewards.

**Step 4: QP Harmonization**
$$\alpha^* = \arg\min_{\alpha \in \Delta^K} \left\|\sum_{k=1}^K \alpha_k \hat{g}_k\right\|^2$$
Finds minimum-norm point in convex hull of normalized gradients — a balanced compromise across rewards.

**Step 5: Rescaling + KL update**
$$d_{\text{final}} = d^* \cdot \bar{n}, \quad \bar{n} = \frac{1}{K}\sum_{k=1}^K \|g_k\|$$
$$\theta \leftarrow \theta - \eta\left(d_{\text{final}} + \beta_{\text{KL}} \cdot \nabla_\theta D_{\text{KL}}(\pi_\theta \|\pi_{\text{ref}})\right)$$

### Amortized Variant

Exploits that DiffusionNFT loss depends on advantage only through affine mapping to $r$. Pre-computes harmonization coefficients via EMA over recent batches, then applies single aggregated coefficient to shared backward pass — reduces overhead from 0.56× to **0.97× relative speed** vs weighted-sum baseline.

## Results

Built on SD3.5 Medium, fine-tuning LoRA (rank 32, alpha 64). Five training rewards: PickScore, HPSv2, CLIPScore, OCR accuracy, GenEval.

| Method | GenEval | OCR | PickScore | CLIPScore | HPSv2.1 | Aesthetic | Composite |
|---|---|---|---|---|---|---|---|
| SD3.5-M + CFG | 0.63 | 0.59 | 22.34 | 0.285 | 0.279 | 5.36 | -0.255 |
| + FlowGRPO (specialist) | 0.95 | 0.66 | 22.51 | 0.293 | 0.274 | 5.32 | +0.120 |
| + DiffusionNFT ‡ (simultaneous) | 0.92 | 0.91 | 21.53 | 0.267 | 0.300 | 6.15 | +0.184 |
| + DiffusionNFT † (sequential) | 0.94 | 0.91 | 23.80 | 0.293 | 0.331 | 6.01 | +1.015 |
| **+ MARBLE** | **0.94** | **0.96** | 22.83 | 0.286 | **0.355** | **6.59** | **+1.116** |

MARBLE achieves **highest Composite score** (+1.116), ranking first on 4 held-out quality metrics (HPSv2.1, Aesthetic, ImageReward, UniReward).

**Training Efficiency**:
- Full harmonization (no amortization): 0.56× speed, 1.14× memory
- Amortized MARBLE: **0.97× speed**, 1.14× memory — nearly same speed as weighted-sum baseline

**Ablations**:
- Without gradient normalization: optimization fails (degenerate coefficients)
- Fixed $\alpha_k=0.2$: moderate degradation (-0.3 to -0.9 points per reward)
- Solve $\alpha$ every step (no amortization): comparable quality but 0.56× speed

## Connections

- **Diffusion + RL**: Bridges [[concepts/diffusion-models|diffusion models]] and [[concepts/rlhf|RL fine-tuning]], extending [[sources/continuous-time-distribution-matching|Continuous-Time DMD]]'s distillation paradigm to multi-reward alignment.
- **Multi-Objective Optimization**: QP harmonization draws from multi-task learning (Desideri 2012, Sener & Koltun 2018). Complements [[sources/general-reasoner|General-Reasoner]]'s cross-domain reward design with principled gradient balancing.
- **Reward Design**: Per-reward decomposition parallels [[sources/repro|RePro]]'s process-level reward lens and [[sources/ruscarl|RuscaRL]]'s rubric-scaffolded multi-criteria evaluation, but for generative rather than reasoning tasks.
- **Efficiency**: Amortized formulation comparable to [[sources/mmtok|MMTok]]'s training-free efficiency and [[sources/roundpipe|RoundPipe]]'s pipeline parallelism — all reduce overhead while maintaining capability.
- **Video Extension**: Reward balancing framework could extend to [[sources/stream-t1|Stream-T1]]'s dual-level reward (spatial + temporal) for unified video generation optimization.

## Citation

```bibtex
@article{zhao2026marble,
  title={MARBLE: Multi-Aspect Reward Balance for Diffusion RL},
  author={Zhao, Canyu and Chen, Hao and Tong, Yunze and Qiao, Yu and Li, Jiacheng and Shen, Chunhua},
  journal={arXiv preprint arXiv:2605.06507},
  year={2026}
}
```

---
*Ingested in Batch 26 (2026-05-05)* | [[index]] | [[concepts/diffusion-models]] | [[concepts/rlhf]] | [[concepts/preference-optimization]]