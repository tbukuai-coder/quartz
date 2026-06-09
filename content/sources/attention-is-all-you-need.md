---
type: source
arxiv_id: "1706.03762"
title: "Attention Is All You Need"
authors: ["Ashish Vaswani", "Noam Shazeer", "Niki Parmar", "Jakob Uszkoreit", "Llion Jones", "Aidan N. Gomez", "Lukasz Kaiser", "Illia Polosukhin"]
date: 2017-06-12
org: "Google Brain / Google Research"
tags: [foundational, architecture, nlp]
upvotes: 121
---

# Attention Is All You Need

> Introduced the **Transformer** architecture — a sequence-to-sequence model based solely on attention mechanisms, dispensing with recurrence and convolutions entirely.

## Key Contributions
- Proposed the **Transformer**, the architecture that underpins virtually all modern LLMs
- Introduced **multi-head self-attention** as the primary computation mechanism
- Demonstrated that attention alone (without RNNs or CNNs) achieves SOTA on machine translation
- Introduced **positional encoding** to inject sequence order information
- Showed massive improvements in training parallelizability and speed

## Method
The Transformer uses an **encoder-decoder** structure where both components are stacks of identical layers. Each layer contains:
1. **Multi-head self-attention** — allows the model to attend to different positions in the input, at different representation subspaces simultaneously
2. **Position-wise feed-forward networks** — two linear transformations with a ReLU activation
3. **Residual connections** and **layer normalization** around each sub-layer

The key innovation is **scaled dot-product attention**: `Attention(Q,K,V) = softmax(QK^T / √d_k)V`, computed in parallel across all positions. Multi-head attention runs this in parallel `h` times with different learned projections.

## Results
- **WMT 2014 English-to-German**: 28.4 BLEU (new SOTA, +2.0 over previous best)
- **WMT 2014 English-to-French**: 41.0 BLEU (new SOTA)
- Trained in 3.5 days on 8 GPUs — significantly faster than competing models
- Also achieved strong results on English constituency parsing

## Connections
- **Foundation for**: [[sources/bert]], [[sources/llama]], [[sources/mistral-7b]], [[sources/mixtral]], and virtually every model in this wiki
- **Key concepts**: [[concepts/transformer-architecture]], [[concepts/self-attention]]
- **Organizations**: [[entities/orgs/google]]

## Citation
> Vaswani et al., "Attention Is All You Need," arXiv:1706.03762, 2017.
> https://huggingface.co/papers/1706.03762
