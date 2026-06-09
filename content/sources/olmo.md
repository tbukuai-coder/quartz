---
type: source
arxiv_id: "2402.00838"
title: "OLMo: Accelerating the Science of Language Models"
authors: ["Dirk Groeneveld", "Iz Beltagy", "Pete Walsh", "Akshita Bhagia", "Rodney Kinney", "Oyvind Tafjord", "Ananya Harsh Jha", "Hamish Ivison", "Ian Magnusson", "Yizhong Wang", "Shane Arora", "David Atkinson", "Russell Authur", "Khyathi Raghavi Chandu", "Arman Cohan", "Jennifer Dumas", "Yanai Elazar", "Yuling Gu", "Jack Hessel", "Tushar Khot", "William Merrill", "Jacob Morrison", "Niklas Muennighoff", "Aakanksha Naik", "Crystal Nam", "Matthew E. Peters", "Valentina Pyatkin", "Abhilasha Ravichander", "Dustin Schwenk", "Saurabh Shah", "Will Smith", "Emma Strubell", "Nishant Subramani", "Mitchell Wortsman", "Pradeep Dasigi", "Nathan Lambert", "Kyle Richardson", "Luke Zettlemoyer", "Jesse Dodge", "Kyle Lo", "Luca Soldaini", "Noah A. Smith", "Hannaneh Hajishirzi"]
date: 2024-02-01
org: "AllenAI"
tags: [pre-training, open-science, open-source, nlp, 2024]
upvotes: 85
---

# OLMo: Accelerating the Science of Language Models

> The first truly open language model release — including training code, training data (Dolma), model weights, evaluation framework, and training logs — designed to accelerate scientific study of language models.

## Key Contributions
- Released OLMo (1B, 7B) as a **fully open** language model: weights, training data (Dolma), training code, evaluation code, and training logs
- Demonstrated competitive performance with other 7B models (LLaMA, Falcon, MPT) while providing complete reproducibility
- Created the Dolma dataset: a 3T token open pretraining corpus with documented curation
- Established a new standard for open-science LLM releases, contrasting with "open-weight" releases (LLaMA, Mistral) that withhold training data and code
- Trained on both NVIDIA (A100) and AMD (MI250X on LUMI supercomputer) GPUs, validating cross-platform training

## Method
**Architecture**: Decoder-only Transformer following the [[sources/llama|LLaMA]] template:
- RMSNorm (pre-normalization)
- SwiGLU activation
- RoPE positional embeddings
- No biases
- 2048 token context length (7B), 4096 vocab size
- 7B: 32 layers, 32 heads, 4096 dim

**Training**:
- Optimizer: AdamW with linear warmup (5K steps) + linear decay to 1/10th peak LR
- ZeRO optimizer (via PyTorch FSDP) for memory-efficient distributed training
- 2T tokens from Dolma (2.46T total with continued training)
- Mixed precision: BF16

**Dolma Dataset** (2T token sample from 3T total):
- Web (Common Crawl via CCNet + quality filtering)
- Code (GitHub, The Stack)
- Academic papers (peS2o from Semantic Scholar)
- Books, Wikipedia, Fandom
- Reddit (Pushshift)
- All sources documented and openly released

**Adaptation**: Instruction tuning using Tülu mix (FLAN, OASST, ShareGPT, etc.) + DPO alignment

## Results
| Model | ARC-E | ARC-C | HellaSwag | PIQA | WinoGrande | MMLU |
|---|---|---|---|---|---|---|
| OLMo-7B | 72.6 | 42.1 | 76.4 | 78.4 | 67.9 | 28.3 |
| LLaMA-7B | 72.5 | 44.5 | 77.8 | 78.5 | 68.0 | 33.3 |
| LLaMA-2-7B | 74.5 | 45.9 | 78.6 | 79.1 | 69.2 | 45.0 |
| MPT-7B | 70.5 | 42.2 | 77.6 | 79.4 | 68.3 | 30.8 |
| Falcon-7B | 69.6 | 42.4 | 76.3 | 79.2 | 66.3 | 27.4 |

OLMo-7B is competitive with other open 7B models, while being the only one with fully open training pipeline.

## Datasets Used
- [[entities/datasets/dolma|Dolma]] — 3T token open pretraining corpus (created alongside OLMo)

## Models Released
- OLMo-1B, OLMo-7B (base)
- OLMo-7B-Instruct (adapted with Tülu SFT + DPO)
- All intermediate checkpoints released

## Connections
- Builds on: [[sources/llama|LLaMA]] (architecture), [[sources/zero-deepspeed|ZeRO/DeepSpeed]] (training framework)
- Extended by: OLMo 2 (improved stability + RLVR), [[sources/olmoe|OLMoE]] (sparse MoE variant), Tülu (adaptation recipes)
- Created: [[entities/datasets/dolma|Dolma]] dataset
- Related: DCLM (data curation benchmark using OLMo)
- Related concepts: [[concepts/pre-training|Pre-training]], [[concepts/training-infrastructure|Training Infrastructure]]
- Ecosystem: Pioneer of "open-science" LLM movement; all artifacts on HF Hub

## Citation
> Groeneveld et al., "OLMo: Accelerating the Science of Language Models," ACL 2024, arXiv:2402.00838, 2024.
