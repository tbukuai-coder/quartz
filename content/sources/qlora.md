---
type: source
arxiv_id: "2305.14314"
title: "QLoRA: Efficient Finetuning of Quantized LLMs"
authors: ["Tim Dettmers", "Artidoro Pagnoni", "Ari Holtzman", "Luke Zettlemoyer"]
date: 2023-05-23
org: "University of Washington"
tags: [peft, quantization, efficiency, 2023]
upvotes: 61
---

# QLoRA: Efficient Finetuning of Quantized Language Models

> Enables fine-tuning a **65B model on a single 48GB GPU** by combining 4-bit quantization with LoRA, preserving full 16-bit fine-tuning performance. Produced Guanaco, which reached 99.3% of ChatGPT performance.

## Key Contributions
- Introduced **4-bit NormalFloat (NF4)** — an information-theoretically optimal 4-bit data type for normally distributed weights
- Introduced **Double Quantization** — quantizing the quantization constants themselves, saving ~0.37 bits per parameter
- Introduced **Paged Optimizers** — using NVIDIA unified memory to handle GPU memory spikes
- Showed that 4-bit quantization + LoRA preserves full 16-bit fine-tuning task performance
- Released **Guanaco** models — 7B to 65B — best open models on the Vicuna benchmark at the time

## Method
QLoRA = 4-bit quantized base model + LoRA adapters trained in BF16:

1. **Quantize** the pre-trained model to 4-bit NF4 precision
2. **Freeze** the quantized weights
3. Add **LoRA adapters** (in BF16) to attention layers
4. **Backpropagate** through the frozen 4-bit weights into the LoRA adapters
5. Use **paged optimizers** (Adam states paged to CPU when GPU OOM)

Key insight: NF4 is optimal for normally distributed data (which neural network weights approximate). Combined with double quantization, this saves ~3× memory over FP16.

## Results
- **Guanaco 65B**: 99.3% of ChatGPT performance on Vicuna benchmark
- **Guanaco 33B**: Competitive with ChatGPT on many tasks
- Fine-tune 65B model on single 48GB GPU (A100) in ~24 hours
- Fine-tune 33B model on single 24GB GPU (A10G)

## Connections
- **Builds on**: [[sources/lora]] (LoRA method)
- **Key concepts**: [[concepts/lora-peft]], [[concepts/quantization]], [[concepts/fine-tuning]]
- **Models**: [[entities/models/guanaco]]
- **Organizations**: University of Washington
- **GitHub**: [artidoro/qlora](https://github.com/artidoro/qlora) (10.9K ⭐)

## Citation
> Dettmers et al., "QLoRA: Efficient Finetuning of Quantized LLMs," arXiv:2305.14314, 2023.
> https://huggingface.co/papers/2305.14314
