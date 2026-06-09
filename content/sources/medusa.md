---
type: source
arxiv_id: "2401.10774"
title: "Medusa: Simple LLM Inference Acceleration Framework with Multiple Decoding Heads"
authors: ["Tianle Cai", "Yuhong Li", "Zhengyang Geng", "Hongwu Peng", "Jason D. Lee", "Deming Chen", "Tri Dao"]
date: 2024-01-19
org: "Together AI / UIUC"
tags: [inference, efficiency, speculative-decoding, 2024]
upvotes: 60
---

# Medusa: Simple LLM Inference Acceleration Framework with Multiple Decoding Heads

> Introduces a **simple, practical** method to accelerate LLM inference by **2.2–3.6×** by adding extra "Medusa heads" that predict multiple future tokens in parallel, verified via tree-based attention — without needing a separate draft model.

## Key Contributions
- **Medusa heads**: Lightweight prediction heads added on top of a frozen LLM backbone, each predicting a future token position (token+1, token+2, ..., token+k)
- **Tree-based attention**: Construct multiple candidate continuations as a tree, verify all branches simultaneously in a single forward pass
- **2.2–3.6× speedup** with negligible quality degradation and minimal VRAM overhead (<1%)
- **Two training modes**:
  - **Medusa-1**: Train heads only (backbone frozen) — lossless inference acceleration
  - **Medusa-2**: Joint training of heads + backbone — higher speedup, needs careful recipe
- **Self-distillation**: Generate training data from the model itself when no external data is available
- No separate draft model needed (unlike standard speculative decoding)

## Method
### Medusa Heads
- Add k extra prediction heads (typically k=5) alongside the original LM head
- Each Medusa head is a single-layer MLP that takes the last hidden state and predicts the token at position +i
- Heads are trained to mimic what the original model would generate at each future position
- Total parameter overhead: ~0.5-1% of backbone parameters

### Tree-Based Attention
- Instead of generating a single continuation, construct a **tree of candidates** from Medusa head predictions
- Use Cartesian product of top-p predictions from each head, pruned by a learned acceptance heuristic
- Process the entire tree in a single forward pass using extended attention masks
- Accept the longest prefix that the original model agrees with
- Average 2.5–3.5 tokens accepted per decoding step (vs 1 in standard autoregressive)

### Training Strategies
- **Medusa-1** (frozen backbone):
  - Freeze backbone LLM, train only Medusa heads
  - Loss: cross-entropy on each head's prediction against actual future tokens
  - Lossless: generation quality identical to original model (accepted tokens are verified)
  
- **Medusa-2** (joint training):
  - Fine-tune backbone + heads together with combined loss
  - Backbone loss weighted to preserve original capabilities
  - Higher acceptance rate but requires more careful training

### Self-Distillation
- Generate training data by running the backbone on random prompts
- Record hidden states and corresponding future tokens
- Train Medusa heads on this self-generated data
- Enables acceleration for any model without external training data

### Typical Acceptance
- Relaxed acceptance criterion: accept tokens if they're "typical" under the model's distribution (not just argmax)
- Increases acceptance rate while maintaining generation quality
- Based on truncation sampling theory

## Results
| Model | Method | Speedup | Overhead |
|---|---|---|---|
| Vicuna-7B | Medusa-1 | 2.18× | <1% VRAM |
| Vicuna-7B | Medusa-2 | 2.83× | <1% VRAM |
| Vicuna-13B | Medusa-2 | 2.69× | <1% VRAM |
| Zephyr-7B | Medusa-2 (self-distill) | 2.36× | <1% VRAM |
| Vicuna-33B | Medusa-2 (self-distill) | 2.29× | <1% VRAM |

- Speedup scales with model size (more memory-bandwidth bound → more benefit)
- Medusa-2 consistently outperforms Medusa-1 by 0.3-0.6× speedup
- Tree structure: 4 levels deep, ~60 candidates per step optimal
- MT-Bench quality maintained across all configurations

## Connections
- **Related to**: Speculative decoding (Leviathan et al., 2022), but requires no draft model
- **Uses**: [[sources/flash-attention]] (efficient attention for tree verification)
- **Key concepts**: [[concepts/speculative-decoding]], [[concepts/flash-attention]]
- **Co-author**: Tri Dao (creator of Flash Attention)
- **GitHub**: [FasterDecoding/Medusa](https://github.com/FasterDecoding/Medusa) — 2.7K ⭐

## Citation
> Cai et al., "Medusa: Simple LLM Inference Acceleration Framework with Multiple Decoding Heads," ICML 2024, arXiv:2401.10774, 2024.
> https://huggingface.co/papers/2401.10774
