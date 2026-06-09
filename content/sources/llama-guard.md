---
type: source
arxiv_id: "2312.06674"
title: "Llama Guard: LLM-based Input-Output Safeguard for Human-AI Conversations"
authors: ["Hakan Inan", "Kartikeya Upasani", "Jianfeng Chi", "Rashi Rungta", "Krithika Iyer", "Yuning Mao", "Michael Tontchev", "Qing Hu", "Brian Fuller", "Davide Testuggine", "James Nez"]
date: 2023-12-07
org: "Meta AI"
tags: [safety, red-teaming, guardrails, classification, 2023]
upvotes: 8
---

# Llama Guard

> The de facto standard safety classifier for LLM deployments — treating content moderation as an instruction-following task with a customizable safety taxonomy. 142K+ HF downloads. Used in TGI, vLLM, and Meta's Llama deployment guides.

## Key Contributions
- **Safety as instruction-following**: Frames content moderation as a text generation task — the LLM classifies input/output as safe/unsafe by generating a verdict
- **Customizable taxonomy**: 6 harm categories (violence, sexual, criminal, weapons, regulated substances, self-harm) — users can add/modify categories via the prompt
- **Dual classification**: Single model classifies both user prompts (input safety) and model responses (output safety) — two-in-one guard
- **State-of-the-art moderation**: Outperforms OpenAI's Moderation API and existing classifiers on ToxicChat and internal benchmarks

## Method
1. **Base model**: Fine-tune Llama 2-7B for classification (later versions use Llama 3)
2. **Input format**: Structured prompt with safety taxonomy description + conversation + classification instruction
3. **Output format**: Model generates "safe" or "unsafe\nS{category_number}" — leverages LLM's instruction-following ability
4. **Training**: Instruction fine-tuning on curated safety classification dataset with examples spanning all taxonomy categories
5. **Customization**: Users modify the taxonomy section of the prompt to add domain-specific categories — no retraining needed

## Results
- **Outperforms OpenAI Moderation API**: Higher F1 on ToxicChat (0.755 vs 0.596) and proprietary benchmark
- Better than keyword-based and embedding-based classifiers
- Customizable taxonomy enables domain-specific safety without retraining
- Low latency — single LLM forward pass for classification

## Models Released
- **Llama Guard** (7B) — original, based on Llama 2
- **Llama Guard 2** (8B) — based on Llama 3, improved MLCommons taxonomy
- **Llama Guard 3** (1B, 8B) — latest version, 142K+ HF downloads

## Impact on the Ecosystem
Llama Guard established the **LLM-as-safety-classifier** paradigm:
- Default safety layer in Meta's Llama deployment guides
- Integrated in TGI, vLLM safety pipelines
- Inspired: ShieldGemma (Google), Aegis (NVIDIA), community safety classifiers
- Concepts: [[concepts/llm-safety|LLM Safety & Guardrails]]

## Connections
- Builds on: [[sources/llama-2|Llama 2]] / [[sources/llama-3|Llama 3]] (base models)
- Related: [[sources/constitutional-ai|Constitutional AI]] (training-time safety vs. inference-time safety)
- Org: [[entities/orgs/meta|Meta AI]]
- Concepts: [[concepts/llm-safety|LLM Safety & Guardrails]]

## Citation
> Inan et al., "Llama Guard: LLM-based Input-Output Safeguard for Human-AI Conversations," arXiv:2312.06674, 2023.
