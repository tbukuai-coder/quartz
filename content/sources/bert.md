---
type: source
arxiv_id: "1810.04805"
title: "BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding"
authors: ["Jacob Devlin", "Ming-Wei Chang", "Kenton Lee", "Kristina Toutanova"]
date: 2018-10-11
org: "Google AI Language"
tags: [foundational, pre-training, nlp]
upvotes: 26
---

# BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding

> Introduced **bidirectional pre-training** of Transformers, showing that a single pre-trained model can be fine-tuned for a wide range of NLP tasks with minimal task-specific architecture.

## Key Contributions
- Introduced **Masked Language Modeling (MLM)** — randomly masking tokens and training the model to predict them, enabling bidirectional context
- Introduced **Next Sentence Prediction (NSP)** as a pre-training objective
- Demonstrated the **pre-train then fine-tune** paradigm that became the standard approach
- Showed that one model architecture can achieve SOTA on 11 different NLP tasks simultaneously
- Released models publicly, catalyzing the open-source NLP revolution

## Method
BERT uses only the **encoder** side of the Transformer. During pre-training:
1. **MLM**: 15% of tokens are masked; the model predicts them using bidirectional context
2. **NSP**: Given two sentences, predict whether the second follows the first

Fine-tuning adds a simple output layer on top and trains end-to-end on task-specific data. This works for classification, sequence labeling, question answering, and more.

Two model sizes released:
- **BERT-Base**: 12 layers, 768 hidden, 12 heads, 110M parameters
- **BERT-Large**: 24 layers, 1024 hidden, 16 heads, 340M parameters

## Results
- **GLUE**: 80.5% → pushed to new SOTA across all tasks
- **SQuAD v1.1**: 93.2 F1 (surpassed human performance)
- **SQuAD v2.0**: 83.1 F1
- **MultiNLI**: 86.7% accuracy

## Connections
- **Builds on**: [[sources/attention-is-all-you-need]] (Transformer encoder)
- **Influenced**: The entire modern NLP ecosystem; pre-train+fine-tune became standard
- **Key concepts**: [[concepts/pre-training]], [[concepts/fine-tuning]], [[concepts/transformer-architecture]]
- **Models**: [[entities/models/bert-model]]
- **Organizations**: [[entities/orgs/google]]

## Citation
> Devlin et al., "BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding," arXiv:1810.04805, 2018.
> https://huggingface.co/papers/1810.04805
