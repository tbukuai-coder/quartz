---
type: concept
tags: [safety, guardrails, moderation, deployment]
---

# LLM Safety & Guardrails

> Techniques for preventing harmful, unsafe, or undesirable LLM outputs — spanning training-time alignment ([[concepts/rlhf|RLHF]], [[concepts/constitutional-ai|Constitutional AI]]) and inference-time classification ([[sources/llama-guard|Llama Guard]]).

## Overview
As LLMs are deployed in production, safety becomes critical. The field distinguishes between **training-time safety** (making the model inherently safer) and **inference-time safety** (filtering inputs/outputs at serving time). Modern deployments typically use both.

## Training-Time Safety
| Approach | How | Paper |
|---|---|---|
| **RLHF** | Train model to avoid harmful outputs via human feedback | [[sources/instructgpt]] |
| **Constitutional AI** | AI-generated critiques enforce safety principles | [[sources/constitutional-ai]] |
| **DPO/KTO** | Preference optimization with safety-focused data | [[concepts/preference-optimization]] |
| **Safety-focused SFT** | Include safety refusal examples in instruction tuning | Standard practice |

## Inference-Time Safety
| Approach | How | Paper |
|---|---|---|
| **[[sources/llama-guard\|Llama Guard]]** | LLM-as-classifier with customizable taxonomy | Inan et al. 2023 |
| **ShieldGemma** | Google's safety classifier | Google 2024 |
| **Keyword filters** | Rule-based content filtering | Baseline approach |
| **Embedding classifiers** | Encode + classify via embeddings | Various |

## The Llama Guard Paradigm
[[sources/llama-guard|Llama Guard]] established the dominant pattern:
1. Define a **safety taxonomy** (categories of harm)
2. Frame classification as **instruction-following** — the LLM generates "safe" or "unsafe\n{category}"
3. **Dual classification** — check both user input and model output in one pass
4. **Customizable** — modify taxonomy via prompt, no retraining needed

## Benchmarkless Safety Comparison

[[sources/benchmarkless-safety-scoring|Benchmarkless Safety Scoring (2026)]] addresses a critical real-world problem: comparing LLMs for safety **before a labeled benchmark exists** for a specific language, sector, or regulatory regime.

The paper formalizes this as **benchmarkless comparative safety scoring** and proposes the **instrumental-validity chain**:
1. Fixed scenario pack, rubric, auditor, judge, sampling config, and rerun budget
2. AUROC-based comparison treating it as a ranking problem
3. Variance decomposition: target-driven variance (signal) vs. auditor/judge artifacts (noise)
4. Local-first scoring: compute scores within scenario subgroups before aggregation to avoid global bias

Key insight: scores are only valid under the specific instrumentation used — changing any component invalidates comparability. This framework provides rigorous deployment evidence in settings where ground-truth safety labels are unavailable.

## Multimodal Domain Generalization Robustness

[[sources/mmdg-benchmark|MMDG-Bench (2026)]] reveals significant robustness challenges in multimodal systems. When evaluated under standardized protocols, many reported performance gains disappear — highlighting that safety and robustness in multimodal deployments require careful, protocol-matched evaluation rather than optimistic single-dataset results.

## Cross-Cultural Safety: XL-SafetyBench

[[sources/xl-safetybench|XL-SafetyBench (2026)]] introduces the first safety evaluation suite that **disentangles jailbreak robustness from cultural sensitivity awareness** across 10 country-language pairs (US, France, Germany, Spain, South Korea, Japan, India, Indonesia, Türkiye, UAE):

### Two Complementary Benchmarks
| Benchmark | What it tests | Evaluation mode |
|---|---|---|
| **Jailbreak Benchmark** | Resisting country-specific adversarial attacks | Adversarial — model should refuse |
| **Cultural Benchmark** | Detecting implicit cultural taboos in innocuous tasks | Natural — model must spot embedded violation |

### Critical Findings
1. **Jailbreak robustness and cultural awareness are NOT coupled** (r = −0.27 for frontier models, n.s.)
2. **English-centric alignment disproportionately benefits US-centric contexts** — all models perform best on US prompts
3. **Local model "safety" is often an illusion**: Low ASR frequently stems from **comprehension failure** (high NSR) rather than principled refusal
4. Open-weight models (Mistral-Large-3, Llama-4-Maverick) fail both dimensions with ASR >90% and CSR <15%
5. Claude family: best jailbreak resistance (2.8–5.9% ASR); Gemini: best cultural awareness (76.1% CSR)

### Metrics
- **ASR** (Attack Success Rate): % jailbreak prompts eliciting harm — **lower = safer**
- **NSR** (Not-Safe Response Rate): % irrelevant/degenerate outputs (not principled refusal) — **lower = better comprehension**
- **CSR** (Cultural Sensitivity Rate): % scenarios where model correctly identifies cultural issue — **higher = better**

The ASR-NSR relationship for local models clusters along **ASR + NSR = 100%** — confirming that apparent safety is driven by generation failure, not alignment.

## Key Papers
- [[sources/llama-guard|Llama Guard]] (2023) — inference-time LLM safety classifier
- [[sources/constitutional-ai|Constitutional AI]] (2022) — training-time AI feedback for safety
- [[sources/instructgpt|InstructGPT]] (2022) — RLHF for alignment including safety
- [[sources/compliance-vs-sensibility|Compliance vs Sensibility]] (2026) — reasoning controllability via CAA steering
- [[sources/benchmarkless-safety-scoring|Benchmarkless Safety Scoring]] (2026) — safety comparison without ground-truth labels
- [[sources/mmdg-benchmark|MMDG-Bench]] (2026) — multimodal domain generalization robustness benchmark
- [[sources/xl-safetybench|XL-SafetyBench]] (2026) — cross-cultural safety evaluation with disaggregated jailbreak and cultural sensitivity metrics


## Efficient Hallucination Detection: First-Token Confidence

[[sources/first-token-knows|First Token Knows (2026)]] demonstrates that a single-decode confidence signal matches multi-sample consistency methods for hallucination detection:
- **φ_first**: Normalized entropy of top-K logits at the first content-bearing answer token
- AUROC 0.820 vs 0.793 (semantic self-consistency) — at 1/11th the cost
- Subsumption analysis: φ_first captures most of semantic agreement's discriminative power (Pearson 0.54–0.76)
- **Practical recommendation**: φ_first should be the default low-cost baseline before any sampling-based uncertainty estimation

## See Also
- [[concepts/rlhf|RLHF]]
- [[concepts/constitutional-ai|Constitutional AI]]
- [[concepts/preference-optimization|Preference Optimization]]
