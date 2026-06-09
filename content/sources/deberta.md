---
type: source
arxiv_id: "2006.03654"
title: "DeBERTa: Decoding-enhanced BERT with Disentangled Attention"
authors: ["Pengcheng He", "Xiaodong Liu", "Jianfeng Gao", "Weizhu Chen"]
date: 2020-06-05
org: "Microsoft"
tags: [foundational, encoder, nlp, attention]
upvotes: 3
---

# DeBERTa: Disentangled Attention Encoder

> Microsoft's enhanced BERT that **disentangles content and position** in the attention mechanism — surpassing human performance on **SuperGLUE** for the first time. DeBERTa-v3 remains the **go-to encoder model** for classification, NLI, and NER tasks on HF Hub (among the most downloaded encoder models).

## Key Contributions
- **Disentangled attention**: Separates content and position into two vectors, computing attention as content-to-content + content-to-position + position-to-content (not combined)
- **Enhanced mask decoder**: Uses absolute position in the decoding layer to complement relative position in attention
- **Scale-efficient**: DeBERTa-Large (304M) surpasses RoBERTa-Large (355M) and matches T5-11B on SuperGLUE
- **First superhuman on SuperGLUE**: 90.3 on SuperGLUE vs. 89.8 human baseline
- **DeBERTa-v3**: Combined with ELECTRA-style replaced token detection for even better efficiency

## Method
### Disentangled Attention
Standard attention: `q·k = (content + position)·(content + position)`

DeBERTa separates this into three terms:
1. **Content-to-content**: How relevant is the content at position j to query at position i?
2. **Content-to-position**: How relevant is the content at position j to the position of query i?
3. **Position-to-content**: How relevant is the position of j to the content at query i?

This provides more expressive attention without increasing parameters significantly.

## Model Family
| Model | Params | SuperGLUE | Key Feature |
|---|---|---|---|
| DeBERTa-Base | 134M | ~85 | Efficient baseline |
| DeBERTa-Large | 304M | ~89 | Near-human |
| DeBERTa-XLarge | 710M | **90.3** | Superhuman |
| DeBERTa-v3-Base | 86M | Strong | ELECTRA-style + smaller |
| DeBERTa-v3-Large | 304M | **91.4** | Best open encoder |

## Impact
- **Most downloaded encoder** for classification/NLI on HF Hub (DeBERTa-v3-base)
- Used as backbone in reward models, classifiers, and quality filters across the ecosystem
- FineWeb-Edu quality classifier is DeBERTa-based
- Standard choice for NLU tasks where decoder-only models are overkill
- Used in DCLM quality filtering pipeline

## Connections
- Builds on: [[sources/bert|BERT]], RoBERTa
- Org: [[entities/orgs/microsoft|Microsoft]]
- Used by: FineWeb-Edu classifier, DCLM filtering
- Concepts: [[concepts/self-attention]], [[concepts/fine-tuning]]

## Citation
> He et al., "DeBERTa: Decoding-enhanced BERT with Disentangled Attention," ICLR 2021, arXiv:2006.03654.
