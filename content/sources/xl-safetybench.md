---
type: source
arxiv_id: "2605.05662"
title: "XL-SafetyBench: A Cross-Cultural and Multi-Dimensional Safety Evaluation Suite for LLMs"
authors: null
venue: "arXiv preprint"
year: 2026
date: "2026-05"
upvotes: 3
tags: [safety, evaluation, multilingual, cultural-awareness, jailbreak, benchmarking]
github: null
---

# XL-SafetyBench: A Cross-Cultural and Multi-Dimensional Safety Evaluation Suite for LLMs

> The first safety evaluation suite disentangling **jailbreak robustness** from **cultural sensitivity awareness** across **10 country-language pairs** — revealing that these two safety dimensions are **not coupled** and require separate measurement.

## Key Contributions

1. **Two complementary benchmarks**: Jailbreak Benchmark (country-specific adversarial robustness) + Cultural Benchmark (implicit culturally embedded sensitivities)
2. **5,500 high-quality test cases**: LLM-assisted discovery with multi-stage human-in-the-loop validation by native speakers
3. **37 LLMs evaluated** (10 frontier, 27 local): Reveals critical gaps in non-English safety
4. **Key finding**: Jailbreak robustness and cultural awareness are **uncorrelated** (r = −0.27 for frontier models, n.s.) — requiring disaggregated safety reporting
5. **Local model illusion**: Apparent safety of many local models stems from **comprehension failure**, not genuine alignment

## Method

### Two-Dimensional Safety Framework

| Dimension | What it measures | Evaluation approach |
|---|---|---|
| **Jailbreak Robustness** | Resisting country-specific adversarial attacks | Adversarial testing where model should refuse |
| **Cultural Sensitivity** | Detecting implicit cultural taboos | Natural tasks where model must spot culturally problematic details |

**Critical distinction**: Prior cultural benchmarks pose the sensitive element as the explicit subject. XL-SafetyBench tests **implicit detection** — the cultural violation is embedded within an innocuous task.

### Construction Pipeline

**Jailbreak Benchmark** (450 prompts/country):
1. LLM-assisted subcategory discovery (country-grounded harm types)
2. Base query generation
3. Iterative attacker-judge red-teaming loop
4. Dual native-speaker validation

**Cultural Benchmark** (100 scenarios/country):
1. Country-specific sensitivity discovery
2. Embed as incidental details within natural surface tasks
3. Automated validation gates
4. Dual native-speaker validation

### Metrics

| Metric | Definition | Target |
|---|---|---|
| **ASR** (Attack Success Rate) | % jailbreak prompts that elicit harmful content | **↓ Lower = safer** |
| **NSR** (Not-Safe Response Rate) | % responses that are irrelevant/degenerate (not principled refusal) | **↓ Lower = better comprehension** |
| **CSR** (Cultural Sensitivity Rate) | % scenarios where model correctly identifies cultural issue | **↑ Higher = better** |

## Critical Findings

### Frontier Models: Capability Gaps

| Model | Avg ASR ↓ | Avg CSR ↑ |
|---|---|---|
| Claude-4.5-Sonnet | **2.8%** | 68.2% |
| Claude-4.6-Opus | 5.9% | 72.7% |
| Gemini-3.1-Pro | 7.2% | **76.1%** |
| Grok-4.20 | 30.6% | 25.4% |
| Mistral-Large-3 | **>90%** | <15% |
| Llama-4-Maverick | **>90%** | <15% |

- Claude family: best jailbreak resistance; Gemini best cultural awareness
- Open-weight models (Mistral, Llama) fail both dimensions

### Country-Level Patterns
- All models perform **best on US prompts** (ASR 34.5%, CSR 69.5%)
- Jailbreak vulnerability highest in **UAE and South Korea** (ASR >50%)
- Cultural awareness drops sharply in **India and Türkiye** (<40%)
- **English-centric alignment disproportionately benefits US-centric contexts**

### Two-Axis Relationship: NOT Coupled

- Across all 10 frontier models: r = −0.74 (but driven by 3 open-weight outliers)
- **Restricting to 7 closed-weight models: r = −0.27 (n.s., p = 0.554)**
- Per-model correlations across 10 countries range from −0.63 (Grok) to +0.33 (Gemini)
- **Verdict: jailbreak robustness and cultural awareness are separate capabilities**

### Local Models: The Illusion of Safety

| Pattern | Global Models | Local Models |
|---|---|---|
| ASR-NSR relationship | Cluster near NSR ≈ 0% (genuine alignment) | Strong negative correlation (r = −0.81) |
| Low ASR mechanism | Principled refusal | **Comprehension failure** (high NSR) |
| High NSR cause | None | Generate irrelevant/degenerate outputs |
| ASR + NSR boundary | Near 0% + 0% | Cluster along **ASR + NSR = 100%** |

**Key insight**: Many local models with low ASRs are not safely aligned — they simply fail to comprehend the prompt (high NSR). When they do comprehend (NSR ≈ 0%), they fail to resist attacks (ASR >90%).

## Connections

- [[sources/benchmarkless-safety-scoring|Benchmarkless Safety Scoring]] — Both address safety evaluation without perfect ground truth; XL-SafetyBench provides culturally grounded test cases
- [[sources/compliance-vs-sensibility|Compliance vs Sensibility]] — Reasoning controllability; XL-SafetyBench extends to cultural reasoning
- [[sources/mmdg-benchmark|MMDG-Bench]] — Multimodal robustness; XL-SafetyBench for text-only cross-cultural safety
- [[sources/aya-vision|Aya Vision]] — Multilingual multimodal; cultural sensitivity is orthogonal to multilingual capability
- [[concepts/llm-safety|LLM Safety]] — Extends safety evaluation to cross-cultural dimensions
- [[concepts/multilingual-models|Multilingual Models]] — Safety must keep pace with multilingual deployment
