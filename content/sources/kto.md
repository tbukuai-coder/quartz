---
type: source
arxiv_id: "2402.01306"
title: "KTO: Model Alignment as Prospect Theoretic Optimization"
authors: ["Kawin Ethayarajh", "Winnie Xu", "Niklas Muennighoff", "Dan Jurafsky", "Douwe Kiela"]
date: 2024-02-02
org: "Contextual AI / Stanford"
tags: [alignment, preference-optimization, kto, 2024]
upvotes: 22
---

# KTO — Kahneman-Tversky Optimization

> Aligns LLMs from binary desirable/undesirable labels (no paired preferences needed) grounded in Kahneman-Tversky prospect theory — matching or beating DPO with simpler, cheaper data. Natively supported in TRL.

## Key Contributions
- **Binary signal alignment**: Only needs "good" or "bad" labels per output — no paired preferences (chosen/rejected) required
- **Human-Aware Loss Functions (HALOs)**: Framework showing that DPO's success partly comes from implicitly modeling human cognitive biases (loss aversion)
- **Prospect theoretic grounding**: Models humans as loss-averse agents per Kahneman-Tversky — losses from bad outputs are weighted more than gains from good outputs
- **Matches or beats DPO** while requiring simpler annotation (binary labels are cheaper to collect than preferences)

## Method
1. **HALOs framework**: Views alignment objectives through the lens of human utility functions. DPO implicitly assumes a logistic utility; KTO explicitly models prospect-theoretic utility with loss aversion
2. **KTO loss**: For each output y given prompt x:
   - If y is desirable: maximize `σ(β · (r_θ(x,y) - z_ref))` where z_ref is a reference point
   - If y is undesirable: minimize `σ(β · (z_ref - r_θ(x,y)))` with higher weight (loss aversion, λ > 1)
   - r_θ is the implicit reward: log(π_θ/π_ref)
3. **No paired data needed**: Each example is independently labeled as good/bad — no need to construct (chosen, rejected) pairs
4. **Reference point**: z_ref estimated as running average of KL divergence from reference policy — serves as the "status quo" in prospect theory

## Results
- Matches DPO on AlpacaEval, MT-Bench with Mistral-7B and Llama-7B
- Outperforms DPO when preference data is converted to unpaired binary labels
- More robust to noisy labels than DPO (loss aversion provides regularization)
- Works with as little as 50% desirable / 50% undesirable data — flexible label ratios
- Natively implemented in TRL as `KTOTrainer`

## Connections
- Extends: [[sources/dpo|DPO]] (paired preferences → binary labels)
- Related: [[sources/orpo|ORPO]] (reference-model-free alignment), [[concepts/dpo|DPO concept]]
- Complements: [[concepts/rlhf|RLHF]], [[concepts/grpo|GRPO]]
- Concepts: [[concepts/preference-optimization|Preference Optimization]]

## Citation
> Ethayarajh et al., "KTO: Model Alignment as Prospect Theoretic Optimization," arXiv:2402.01306, 2024.
