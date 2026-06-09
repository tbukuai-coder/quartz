---
type: source
arxiv_id: "2403.07691"
title: "ORPO: Monolithic Preference Optimization without Reference Model"
authors: ["Jiwoo Hong", "Noah Lee", "James Thorne"]
date: 2024-03-12
org: "KAIST"
tags: [alignment, preference-optimization, efficiency, 2024]
upvotes: 72
---

# ORPO — Odds Ratio Preference Optimization

> Combines SFT and preference alignment in a single training stage without a reference model — surpasses DPO+SFT pipeline with half the compute. Natively in TRL.

## Key Contributions
- **Monolithic optimization**: Merges SFT and preference alignment into one loss function — eliminates the 2-stage SFT→DPO pipeline
- **Reference-model-free**: No reference model needed (unlike DPO which requires a frozen reference) — halves GPU memory for alignment
- **Odds ratio penalty**: Uses log-odds ratio to penalize disfavored generations — a mild penalty during SFT is sufficient for alignment
- **Half the compute** of SFT+DPO pipeline with equal or better performance

## Method
1. **Insight**: During SFT, the model already learns to distinguish between good and bad text — a small additional penalty for disfavored styles is enough for alignment
2. **ORPO loss**: Standard SFT cross-entropy loss + odds ratio penalty:
   - `L = L_SFT + λ · L_OR`
   - `L_OR = -log σ(log(odds(y_w|x) / odds(y_l|x)))`
   - Where odds(y|x) = P(y|x) / (1 - P(y|x))
3. **No reference model**: The odds ratio naturally provides a relative comparison between chosen and rejected — no need for π_ref
4. **Single stage**: Train once with both chosen and rejected examples + the preference penalty — no separate SFT warmup needed

## Results
- Outperforms SFT+DPO pipeline on AlpacaEval 2.0, IFEval, MT-Bench
- **Phi-2 (2.7B) + ORPO**: 12.20% on AlpacaEval 2.0 (vs. 11.07% with SFT+DPO)
- **Llama-2-7B + ORPO**: Competitive with SFT+DPO at half the compute
- **Mistral-7B + ORPO**: 14.43% AlpacaEval (strong for 7B models)
- Natively implemented in TRL as `ORPOTrainer`

## Datasets Used
- UltraFeedback (preference data) — same data used for DPO baseline comparison

## Connections
- Simplifies: [[sources/dpo|DPO]] (removes reference model + SFT stage)
- Related: [[sources/kto|KTO]] (different simplification — binary labels), [[concepts/dpo|DPO]]
- Uses: [[entities/datasets/ultrafeedback|UltraFeedback]] for evaluation
- Concepts: [[concepts/preference-optimization|Preference Optimization]]

## Citation
> Hong et al., "ORPO: Monolithic Preference Optimization without Reference Model," arXiv:2403.07691, 2024.
