---
type: source
arxiv_id: "1910.01108"
title: "DistilBERT, a distilled version of BERT: smaller, faster, cheaper and lighter"
authors: ["Victor Sanh", "Lysandre Debut", "Julien Chaumond", "Thomas Wolf"]
date: 2019-10-02
org: "Hugging Face"
tags: [distillation, efficiency, bert, foundational]
upvotes: 22
---

# DistilBERT

> The first large-scale application of knowledge distillation to pretrained Transformers — 40% smaller, 60% faster, retaining 97% of BERT's performance. A Hugging Face-authored paper. 10.7M+ HF downloads.

## Key Contributions
- **Triple distillation loss**: Combines MLM loss + distillation loss (soft labels from teacher) + cosine embedding loss (hidden state alignment)
- **40% size reduction**: 6 layers instead of BERT's 12, removing token-type embeddings and pooler
- **60% faster inference**: Directly proportional to layer reduction
- **97% performance retention**: On GLUE benchmark, DistilBERT retains 97% of BERT-base performance
- **First HF-authored model paper**: Established Hugging Face as a research lab, not just a platform

## Method
1. **Teacher**: BERT-base-uncased (12 layers, 110M params)
2. **Student**: DistilBERT (6 layers, 66M params) — initialized from every other layer of the teacher
3. **Training losses**:
   - **Distillation loss**: KL divergence between teacher and student soft predictions (with temperature T=8)
   - **MLM loss**: Standard masked language modeling on same data
   - **Cosine embedding loss**: Align student hidden states with teacher hidden states
4. **Training data**: Same as BERT — English Wikipedia + BookCorpus
5. **Architecture changes**: Remove token-type embeddings, remove pooler, half the layers

## Results
- **GLUE**: 97% of BERT-base (77.0 vs 79.5 avg)
- **SQuAD v1.1**: 86.9 F1 vs BERT's 88.5 F1
- **40% smaller** (66M vs 110M), **60% faster**
- On-device deployment feasible (iPhone inference)
- Spawned: DistilRoBERTa, DistilGPT2, DistilBART

## Impact on the Ecosystem
- Top-5 most downloaded model on HF Hub (10.7M+ downloads)
- Established knowledge distillation as standard NLP technique
- Proved HF could produce research, not just tools
- Template for subsequent distillation work: [[sources/smollm2|SmolLM2]], [[sources/zephyr|Zephyr]]

## Connections
- Builds on: [[sources/bert|BERT]] (teacher model)
- Concepts: [[concepts/distillation|Distillation]], [[concepts/fine-tuning|Fine-tuning]]
- Org: [[entities/orgs/huggingface|Hugging Face]]
- Extended by: DistilRoBERTa, DistilGPT2 (same technique, different teachers)

## Citation
> Sanh et al., "DistilBERT, a distilled version of BERT: smaller, faster, cheaper and lighter," NeurIPS 2019 Workshop, arXiv:1910.01108.
