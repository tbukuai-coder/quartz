---
type: source
arxiv_id: "2605.05166"
title: "The First Token Knows: Single-Decode Confidence for Hallucination Detection"
authors: ["Mina Gabriel"]
venue: "arXiv preprint"
year: 2026
date: "2026-05"
org: null
upvotes: 1
tags: [hallucination, uncertainty, confidence, evaluation, efficiency]
github: null
---

# The First Token Knows: Single-Decode Confidence for Hallucination Detection

> First-token confidence (φ_first) — the normalized entropy of top-K logits at the first content-bearing answer token — **matches or exceeds semantic self-consistency** for hallucination detection at **1/11th the generation cost**, without requiring multi-sample generation or NLI inference.

## Key Contributions

1. **φ_first metric**: Normalized entropy of top-K logits at the first content-bearing answer token of a single greedy decode — a zero-overhead confidence signal
2. **Matches semantic self-consistency**: Mean AUROC 0.820 vs 0.793 (semantic agreement) and 0.791 (surface-form self-consistency) across 3 models and 2 benchmarks
3. **11× cost reduction**: Single greedy decode vs 1 greedy + 10 sampled generations + NLI clustering
4. **Subsumption analysis**: Pearson correlation 0.54–0.76 with semantic agreement; logistic ensemble yields only +0.02 AUROC improvement — φ_first captures most of semantic agreement's discriminative power
5. **Length confound eliminated**: Partial correlation analysis shows apparent φ_first–length association disappears after controlling for correctness

## Method

### φ_first Computation
Given logits ℓ_t at decode step t, let t* be the first content-bearing answer token. φ_first is:

```
φ_first = 1 - H_K(p_t*) / log(K)
```

Where H_K is the entropy computed over the top-K softmax probabilities. High φ_first = low entropy = high confidence = less likely to be hallucinating.

### Key Insight
The first content token concentrates the model's uncertainty about the entire answer. If the model "knows" the answer, the first token distribution is sharp; if uncertain, it's diffuse — and this signal is as informative as sampling 10+ completions and clustering them.

## Results

### Main Results (AUROC for hallucination detection)
| Method | Llama-3.1-8B | Mistral-7B-v0.3 | Qwen2.5-7B | Mean |
|---|---|---|---|---|
| φ_first (ours) | 0.834 | 0.808 | 0.818 | **0.820** |
| Semantic Agreement | 0.804 | 0.781 | 0.795 | 0.793 |
| Surface-form SC | 0.796 | 0.779 | 0.797 | 0.791 |
| Verbalized Confidence | 0.720 | 0.695 | 0.741 | 0.719 |

### Cost Comparison
| Method | Forward Passes | Additional Inference | Relative Cost |
|---|---|---|---|
| **φ_first** | 1 (greedy) | None | **1×** |
| Surface-form SC | 11 (1 greedy + 10 sampled) | None | 11× |
| Semantic SC | 11 | + NLI clustering | ~15× |

### Practical Recommendation
φ_first should be reported as a **default, low-cost baseline** before invoking any sampling-based uncertainty estimation. It's free (computed from the existing greedy decode) and captures most of the signal.

## Connections

- [[concepts/llm-evaluation|LLM Evaluation]] — Efficient hallucination detection without multi-sample overhead
- [[concepts/llm-safety|LLM Safety]] — Detecting unreliable outputs at inference time
- [[sources/oscar-vlm|OSCAR]] — Both address hallucination; OSCAR uses MCTS+DPO for VLMs, First Token Knows uses single-decode confidence
- [[sources/compliance-vs-sensibility|Compliance vs Sensibility]] — Both study internal model signals for output quality
