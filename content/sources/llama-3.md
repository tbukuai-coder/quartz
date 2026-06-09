---
type: source
arxiv_id: "2407.21783"
title: "The Llama 3 Herd of Models"
authors: ["Abhimanyu Dubey", "et al. (527 authors)"]
date: 2024-07-23
org: "Meta AI"
tags: [open-models, pre-training, multimodal, 2024]
upvotes: 118
---

# The Llama 3 Herd of Models

> Meta's **third-generation** open models scaling to **405B parameters** with 128K context, natively supporting multilinguality, coding, reasoning, tool usage, and multimodal capabilities — competitive with GPT-4 class models.

## Key Contributions
- Scaled open models to **405B dense parameters** — the largest open-weight model at release
- Trained on **15T+ tokens** of multilingual data
- Native support for **128K token context**
- Multimodal through **compositional approach**: plugging in image, video, and speech encoders
- Extensive post-training pipeline: SFT, rejection sampling, DPO, and tool-use training
- Released 8B, 70B, and 405B variants — all fully open weights

## Method
### Pre-training
- **15T+ tokens** of curated data (vs. 2T for Llama 2)
- Architecture: standard dense Transformer with GQA, RoPE, SwiGLU, RMSNorm
- 405B model: 126 layers, 128 attention heads, 16K hidden dim
- 128K context via progressive context extension during training

### Post-training
1. **SFT** on high-quality instruction data
2. **Rejection sampling** using reward model
3. **DPO** for final alignment
4. **Tool-use training**: code interpreter, search, mathematical tools
5. **System prompt adherence** training

### Multimodal
- Image encoder (cross-attention adapter)
- Video encoder (temporal aggregation)
- Speech encoder (streaming adapter)
- Compositional approach: each modality adapter is trained separately

## Models Released
| Model | Params | Context | Multimodal |
|---|---|---|---|
| Llama 3.1 8B | 8B | 128K | Text only |
| Llama 3.1 70B | 70B | 128K | Text only |
| Llama 3.1 405B | 405B | 128K | Text only |
| Llama 3.2 1B | 1B | 128K | Text only |
| Llama 3.2 3B | 3B | 128K | Text only |
| Llama 3.2 11B | 11B | 128K | Vision + Text |
| Llama 3.2 90B | 90B | 128K | Vision + Text |

## Results
- Llama 3.1 405B is competitive with **GPT-4** and **Claude 3.5 Sonnet** on many benchmarks
- Llama 3.1 70B competitive with **GPT-4o-mini**
- Llama 3.1 8B outperforms most open 7B models

## Connections
- **Builds on**: [[sources/llama]], [[sources/llama-2]] (previous generations)
- **Uses**: [[concepts/dpo]], [[concepts/rlhf]], [[concepts/gqa]], [[concepts/flash-attention]]
- **Continued by**: [[sources/llama-4]] (MoE architecture shift)
- **Models**: [[entities/models/llama]]
- **Organizations**: [[entities/orgs/meta]]

## Citation
> Dubey et al., "The Llama 3 Herd of Models," arXiv:2407.21783, 2024.
> https://huggingface.co/papers/2407.21783
