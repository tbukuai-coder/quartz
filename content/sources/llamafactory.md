---
type: source
arxiv_id: "2403.13372"
title: "LlamaFactory: Unified Efficient Fine-Tuning of 100+ Language Models"
authors: ["Yaowei Zheng", "Richong Zhang", "Junhao Zhang", "Yanhan Ye", "Zheyan Luo"]
date: 2024-03-19
org: "Renmin University of China"
tags: [tools, fine-tuning, peft, 2024]
upvotes: 183
---

# LlamaFactory: Unified Efficient Fine-Tuning of 100+ Language Models

> A unified **no-code fine-tuning framework** supporting 100+ models with LoRA, QLoRA, full fine-tuning, RLHF, DPO, and more — the most starred fine-tuning tool on GitHub (70K+ ⭐).

## Key Contributions
- Unified interface for fine-tuning **100+ LLMs** across multiple methods
- **LlamaBoard**: web-based UI enabling fine-tuning without coding
- Supports: full fine-tuning, [[concepts/lora-peft|LoRA]], [[concepts/quantization|QLoRA]], RLHF/PPO, [[concepts/dpo|DPO]], ORPO, and more
- Integrates with FlashAttention, DeepSpeed, FSDP for distributed training
- Dataset preprocessing, evaluation, and model export built-in
- **70,500+ GitHub stars** — most popular LLM fine-tuning tool

## Method
### Architecture
- Modular design: model loader, data processor, training module, evaluation module
- Supports Hugging Face Transformers models natively
- Automatic template selection for chat models
- Mixed-precision training (BF16, FP16, INT4, INT8)

### Supported Training Methods
| Method | Type | Description |
|---|---|---|
| Full Fine-tuning | Standard | Update all parameters |
| LoRA / QLoRA | PEFT | Low-rank adaptation |
| SFT | Alignment | Supervised fine-tuning |
| RLHF (PPO) | Alignment | RL from human feedback |
| DPO | Alignment | Direct preference optimization |
| ORPO | Alignment | Odds ratio preference optimization |
| KTO | Alignment | Kahneman-Tversky optimization |

### LlamaBoard UI
- Web interface for configuring training without code
- Dataset selection, hyperparameter tuning, live monitoring
- Export to GGUF, ONNX, or Hugging Face Hub

## Connections
- **Implements**: [[concepts/lora-peft]], [[concepts/quantization]], [[concepts/dpo]], [[concepts/rlhf]], [[concepts/instruction-tuning]]
- **Supports models**: [[entities/models/llama]], [[entities/models/mistral]], [[entities/models/qwen]], [[entities/models/gemma]], [[entities/models/deepseek]], and 100+ more
- **Related**: [[entities/orgs/huggingface]] (TRL library, alternative approach)
- **GitHub**: [hiyouga/LLaMA-Factory](https://github.com/hiyouga/LLaMA-Factory) (70.5K ⭐)

## Citation
> Zheng et al., "LlamaFactory: Unified Efficient Fine-Tuning of 100+ Language Models," arXiv:2403.13372, 2024.
> https://huggingface.co/papers/2403.13372
