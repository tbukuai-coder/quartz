---
type: source
arxiv_id: "2101.03961"
title: "Switch Transformers: Scaling to Trillion Parameter Models with Simple and Efficient Sparsity"
authors: ["William Fedus", "Barret Zoph", "Noam Shazeer"]
date: 2021-01-11
org: "Google Brain"
tags: [moe, architecture, scaling, foundational]
upvotes: 13
---

# Switch Transformers

> The foundational modern MoE paper — simplified routing to top-1 expert selection ("Switch"), enabling trillion-parameter models with 7× pretraining speedup. The ancestor of Mixtral and DeepSeek-V3.

## Key Contributions
- **Top-1 routing ("Switch")**: Route each token to a single expert instead of top-2+ — simplest possible MoE, yet effective
- **Auxiliary load-balancing loss**: Small auxiliary loss to prevent expert collapse — adopted by Mixtral, refined by DeepSeek-V3
- **Trillion-parameter demonstration**: First to show MoE reliably scales to 1T+ parameters
- **7× pretraining speedup**: Over T5-Base at equivalent quality with same compute budget
- **bf16 stability**: Showed selective bf16 casting stabilizes MoE training (expert computations in bf16, routing in fp32)

## Method
1. **Architecture**: Standard Transformer with FFN layers replaced by Switch FFN layers. Each Switch FFN has N expert FFNs + a learned router
2. **Router**: Linear layer mapping hidden state → N-dimensional logits. Token routed to argmax expert (top-1)
3. **Load balancing**: Auxiliary loss = α · Σ(f_i · P_i) where f_i is fraction of tokens to expert i, P_i is average routing probability to expert i. Encourages uniform distribution
4. **Capacity factor**: Each expert has a buffer size = (tokens/experts) × capacity_factor. Overflow tokens dropped — simple but effective
5. **Expert parallelism**: Experts distributed across devices. All-to-all communication for token routing

## Results
- **Switch-Base (128 experts)**: 7× faster pretraining than T5-Base at same quality
- **Switch-Large**: Outperforms T5-Large with same compute
- **Multilingual (mT5-Base vs Switch-mT5)**: Consistent gains across 101 languages
- **Distillation**: Can distill Switch model into dense model, retaining 30% of gains
- **Trillion-parameter model**: Successfully trained 1.6T param model (stable training)

## Impact on the Ecosystem
Switch Transformer established the MoE paradigm that all modern MoE models follow:
- [[sources/mixtral|Mixtral]] uses top-2 routing (evolution of Switch's top-1)
- [[sources/deepseek-v3|DeepSeek-V3]] refined the load-balancing to auxiliary-loss-free
- [[sources/llama-4|Llama 4]] adopted MoE architecture
- Google released Switch models on HF Hub

## Connections
- Extended by: [[sources/mixtral|Mixtral]], [[sources/deepseek-v3|DeepSeek-V3]], [[sources/llama-4|Llama 4]]
- Concepts: [[concepts/mixture-of-experts|Mixture of Experts]], [[concepts/scaling-laws|Scaling Laws]]
- Org: [[entities/orgs/google|Google]]

## Citation
> Fedus et al., "Switch Transformers: Scaling to Trillion Parameter Models with Simple and Efficient Sparsity," JMLR 2022, arXiv:2101.03961.
