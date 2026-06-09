---
type: source
arxiv_id: "2407.21772"
title: "ShieldGemma: Generative AI Content Moderation Based on Gemma"
authors: ["Wenjun Zeng", "Yuchi Liu", "Ryan Mullins"]
date: 2024-07-31
org: "Google"
tags: [safety, content-moderation, gemma, 2024]
upvotes: 14
---

# ShieldGemma

> Google's LLM-based safety content moderation models built on Gemma2, outperforming existing solutions including Llama Guard and OpenAI moderation API across harm types.

## Key Contributions
- Released **ShieldGemma** models (2B, 9B, 27B) for content moderation — detecting sexually explicit, dangerous, harassment, and hate speech content
- Outperforms **Llama Guard** and **OpenAI moderation API** on comprehensive safety benchmarks
- Demonstrated that **synthetic data** can effectively train safety classifiers with strong generalization
- Both **input (prompt) and output (response)** classification supported
- Built on [[sources/gemma-2|Gemma 2]] architecture — benefits from Gemma's strong language understanding

## Method
**Instruction-tuned classifier**: ShieldGemma is fine-tuned as a binary/multi-class classifier where the model reads a prompt/response and outputs a safety label. Uses:
1. **Curated safety taxonomy**: Four primary harm categories (sexually explicit, dangerous, harassment, hate speech)
2. **Synthetic training data**: Generated adversarial and edge-case examples using LLMs
3. **Multi-task training**: Joint training on input classification and output classification
4. **Gemma 2 backbone**: Leverages pre-trained language understanding for nuanced safety judgments

## Results
- **F1 scores**: ShieldGemma-27B achieves highest F1 across all harm categories vs baselines
- **vs Llama Guard**: +3–5 F1 points improvement on average
- **vs OpenAI moderation**: Significantly better on sexually explicit and dangerous content
- **Generalization**: Strong OOD performance even when trained on synthetic data
- **Scale**: 2B model already competitive, 27B reaches best performance

## Models Released
- ShieldGemma-2B, ShieldGemma-9B, ShieldGemma-27B (open weights)

## Connections
- **Built on**: [[sources/gemma-2|Gemma 2]], [[entities/orgs/google|Google]]
- **Related**: [[sources/llama-guard|Llama Guard]] (Meta's safety classifier), [[concepts/llm-safety|LLM Safety]]
- **Complements**: [[sources/constitutional-ai|Constitutional AI]] (training-time safety vs inference-time moderation)
- **Used with**: Any LLM deployment pipeline as an input/output filter

## Citation
> Zeng et al., "ShieldGemma: Generative AI Content Moderation Based on Gemma," arXiv:2407.21772, 2024.
