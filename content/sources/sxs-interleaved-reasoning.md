---
type: source
arxiv_id: "2605.03314"
title: "When to Think, When to Speak: Learning Disclosure Policies for LLM Reasoning"
authors: ["Jiaqi Wei", "Xuehang Guo", "Pengfei Yu", "Xiang Zhang", "Wanli Ouyang", "Siqi Sun", "Qingyun Wang", "Chenyu You"]
venue: "arXiv preprint"
year: 2026
date: "2026-05"
org: null
upvotes: 1
tags: [reasoning, inference-efficiency, interleaved-generation, disclosure-policy, streaming]
github: null
---

# Side-by-Side (SxS) Interleaved Reasoning: Learning Disclosure Policies for LLM Reasoning

> Makes disclosure timing a **controllable decision** within standard autoregressive generation — interleaving private reasoning with user-visible partial answers to mitigate the "silence tax" of single-stream CoT, improving accuracy–latency Pareto trade-offs on AIME25 and GPQA-Diamond.

## Key Contributions

1. **Silence tax problem**: In single-stream CoT, additional deliberation delays all content delivery; naive early streaming risks premature commitments that bias subsequent generation
2. **Side-by-Side (SxS) format**: Interleaves private reasoning (think) with public answer disclosures (speak) in the same context — content released only when supported by reasoning so far
3. **Entailment-aligned SFT data**: Matches answer prefixes to supporting reasoning prefixes using NLI verification — ensures early disclosures are logically grounded
4. **Two-stage training**: SFT teaches dual-action format, then GRPO-based RL restores task accuracy and improves accuracy–latency trade-off
5. **Pareto improvement**: Better accuracy–content-latency trade-offs on AIME25 and GPQA-Diamond across Qwen3-30B-A3B (MoE) and Qwen3-4B (dense)

## Method

### The Silence Tax Problem
Standard "think-then-speak":
```
[Think: 500 tokens of reasoning...] [Speak: final answer]
```
User waits for ALL reasoning before seeing ANY content. But premature streaming risks wrong commitments.

### SxS Interleaved Reasoning
```
[Think: partial reasoning] [Speak: supported partial answer]
[Think: more reasoning]   [Speak: refinement/extension]
[Think: final reasoning]  [Speak: complete answer]
```

### Training Pipeline
1. **Data construction**: Given (input, reasoning, answer), use entailment detection (GPT-OSS-120B) to align answer segments to reasoning prefixes that support them
2. **SFT**: Train model on interleaved format to acquire dual-action semantics (think/speak)
3. **RL (GRPO)**: Outcome-based reward + optional granularity shaping to recover accuracy and learn optimal disclosure timing

### Key Insight
Disclosure timing is a policy decision — the model learns WHEN reasoning sufficiently supports a partial answer, releasing content incrementally while continuing to deliberate.

## Results

### AIME25 (Qwen3-30B-A3B)
| Method | Accuracy | Average Response Index ↓ |
|---|---|---|
| Standard CoT | 56.7% | 1.00 (normalized) |
| SxS (SFT only) | 43.3% | 0.52 |
| **SxS (SFT+RL)** | **53.3%** | **0.58** |

- SxS recovers most accuracy while delivering content 42% earlier
- Pareto-dominant: better latency at comparable accuracy

### GPQA-Diamond (OOD transfer)
- Similar Pareto improvements on out-of-domain scientific reasoning
- Format generalizes beyond math to knowledge-intensive tasks

### RL Does Not Degrade Granularity
- With auxiliary shaping, RL maintains frequent interleaving
- Without shaping, RL tends toward fewer but larger speak blocks (still better than standard CoT latency)

## Connections

- [[sources/interleaved-reasoning|Interleaved Reasoning]] — Both interleave think/answer; Interleaved Reasoning focuses on accuracy gains, SxS on latency–accuracy trade-offs
- [[sources/lenvm|LenVM]] — Both control generation behavior; LenVM controls length via value estimation, SxS controls disclosure timing
- [[concepts/chain-of-thought|Chain-of-Thought]] — SxS extends CoT with controllable disclosure
- [[concepts/test-time-compute|Test-Time Compute]] — Enables streaming test-time compute without forcing user to wait
- [[sources/deepseek-r1|DeepSeek-R1]] — Single-stream reasoning model that would benefit from SxS-style disclosure
