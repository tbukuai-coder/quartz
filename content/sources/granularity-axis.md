---
type: source
arxiv_id: "2605.06196"
title: "The Granularity Axis: A Micro-to-Macro Latent Direction for Social Roles in Language Models"
authors: ["Chonghan Qin", "Xiachong Feng", "Ziyun Song", "Xiaocheng Feng", "Jing Xiong", "Lingpeng Kong"]
venue: "arXiv preprint"
year: 2026
date: "2026-05"
org: null
upvotes: 5
tags: [interpretability, activation-steering, social-roles, representation-geometry, controllability]
github: "https://github.com/qinchonghanzuibang/Granularity-Axis"
---

# The Granularity Axis: A Micro-to-Macro Latent Direction for Social Roles in LLMs

> LLMs encode social role granularity as a **single, ordered, causally manipulable direction** in activation space — the contrast-based Granularity Axis aligns with PC1 at cosine 0.972 and accounts for 52.6% of variance, enabling activation steering that shifts responses from individual to institutional perspectives.

## Key Contributions

1. **Discovery of the Granularity Axis**: A single latent direction (PC1 of role representation space) encodes social role granularity from micro (individual) to macro (institutional/national)
2. **Dominant geometric structure**: Cosine alignment 0.972 with PC1, explains 52.6% of variance in Qwen3-8B — granularity is THE organizing dimension for social roles
3. **Causal manipulation**: Activation steering along the axis shifts response granularity predictably (Llama: 2.00 → 3.17 on 5-point scale under positive steering)
4. **Cross-model transfer**: Structure replicates in Llama-3.1-8B-Instruct with same monotonic ordering
5. **Methodological contribution**: Contrast-based axis definition + PCA validation + steering evaluation framework for interpretability research

## Method

### Axis Construction
1. Collect 91,200 role-conditioned responses across 75 social roles (5 granularity levels × 15 roles)
2. Extract hidden states at each layer, compute role-level mean representations
3. Define Granularity Axis = mean(macro-role states) − mean(micro-role states)
4. Validate: axis aligns with PC1 at cosine 0.972

### Five Granularity Levels
| Level | Type | Examples |
|---|---|---|
| L1 (Micro) | Individual | Worried Parent, First-Gen Student |
| L2 | Group/Community | Neighborhood Association, Local Church |
| L3 (Meso) | Organization | Hospital Network, Tech Startup |
| L4 | Institution/Systemic | Federal Reserve, Supreme Court |
| L5 (Macro) | Nation/Super-Actor | EU, United Nations, China |

### Activation Steering
- Inject axis direction (scaled by α) at each generation step
- Positive α → macro-level (institutional/policy) responses
- Negative α → micro-level (personal/experiential) responses

## Results

- **Monotonic ordering**: Role projections increase consistently L1 → L5 across both models
- **Stability**: Holds across layers 8–35 (Qwen), prompt variants, score-filtered subsets
- **Causal effect**: Llama shifts from 2.00 to 3.17 on granularity scale under positive steering
- **Model-dependent controllability**: Qwen (default macro regime) has less headroom for positive steering; Llama responds more uniformly
- **Human evaluation**: Pairwise preference rate up to 90.3% alignment with predicted direction

## Connections

- [[sources/compliance-vs-sensibility|Compliance vs Sensibility]] — Both study internal model directions for behavioral control; Compliance uses CAA for safety, Granularity uses contrast for social roles
- [[sources/reasoning-vectors|Reasoning Vectors]] — Both apply task arithmetic / activation steering; Reasoning Vectors for CoT transfer, Granularity for social role control
- [[concepts/llm-safety|LLM Safety]] — Social role steering has safety implications (e.g., institutional vs individual framing)
