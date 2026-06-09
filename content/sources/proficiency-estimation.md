---
type: source
arxiv_id: "2605.03848"
title: "Parameter-Efficient Multi-View Proficiency Estimation: From Discriminative Classification to Generative Feedback"
authors: ["Edoardo Bianchi", "Antonio Liotta"]
venue: "arXiv preprint"
year: 2026
date: "2026-05"
org: null
upvotes: 4
tags: [video-understanding, multi-view, action-quality, parameter-efficient, embodied-ai]
github: null
---

# Parameter-Efficient Multi-View Proficiency Estimation

> Three methods — SkillFormer, PATS, and ProfVLM — achieve SOTA accuracy on **Ego-Exo4D** proficiency estimation with up to **20× fewer trainable parameters** and **3× fewer training epochs** than video-transformer baselines, while moving from classification toward interpretable generative feedback.

## Key Contributions

1. **SkillFormer**: Parameter-efficient discriminative architecture with selective multi-view fusion via gated cross-attention and LoRA-adapted TimeSformer backbone
2. **PATS (Proficiency-Aware Temporal Sampling)**: Preserves locally dense excerpts of fundamental movements rather than uniform sampling — captures timing and execution quality
3. **ProfVLM**: First vision–language model for proficiency estimation that produces both a label AND expert-style textual feedback through conditional language generation
4. **Efficiency**: 20× fewer trainable parameters, 3× fewer epochs vs video-transformer baselines
5. **Paradigm shift**: From closed-set classification → interpretable generative feedback for coaching/rehabilitation

## Method

### Three Complementary Approaches

| Method | Type | Key Innovation | Output |
|---|---|---|---|
| SkillFormer | Discriminative | Gated cross-attention for selective multi-view fusion | Proficiency label |
| PATS | Sampling | Locally dense temporal excerpts at key moments | Better input for any model |
| ProfVLM | Generative | Cross-view projector + language backbone | Label + textual feedback |

### SkillFormer
- Shared TimeSformer backbone (LoRA-adapted) encodes each of V synchronized views
- Gated cross-attention selectively fuses informative views
- Learns WHICH views are relevant for WHICH aspects of proficiency

### PATS (Proficiency-Aware Temporal Sampling)
- Problem: Uniform sampling misses brief critical moments (a shot, a climbing move)
- Solution: Identify fundamental movement segments, sample densely within them
- Preserves the temporal micro-structure where proficiency differences manifest

### ProfVLM
- Gated cross-view projector aligns multi-view features
- Compact language backbone (autoregressive) generates:
  1. Proficiency classification token
  2. Expert-style feedback text explaining the assessment
- First model to provide actionable coaching feedback, not just a label

## Results

### Ego-Exo4D Proficiency Estimation
- All three methods: SOTA with dramatically fewer parameters
- SkillFormer: Best accuracy among discriminative methods
- PATS: Improves any base model when used as temporal sampling strategy
- ProfVLM: Competitive accuracy + unique feedback generation capability

### Key Lessons
1. Not all views are equally informative — selective fusion outperforms naive concatenation
2. Temporal density at critical moments matters more than broad uniform coverage
3. Generative output enables interpretable feedback without sacrificing classification accuracy

## Connections

- [[concepts/vision-language-models|Vision-Language Models]] — ProfVLM applies VLM architecture to action quality assessment
- [[sources/mmtok|MMTok]] — Both address efficiency in video understanding; MMTok prunes tokens, PATS improves temporal sampling
- [[concepts/multimodal-models|Multimodal Models]] — Multi-view fusion as specialized multimodal problem
