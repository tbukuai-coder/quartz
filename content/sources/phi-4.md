---
type: source
arxiv_id: "2412.08905"
title: "Phi-4 Technical Report"
authors: ["Marah Abdin", "et al. (Microsoft Research)"]
date: 2024-12-11
org: "Microsoft Research"
tags: [open-models, synthetic-data, pre-training, reasoning, 2024]
upvotes: 123
---

# Phi-4 Technical Report

> A **14B parameter** language model that **surpasses its GPT-4 teacher** on STEM reasoning by strategically incorporating synthetic data throughout pretraining — demonstrating that data quality innovations can overcome the limitations of model scale.

## Key Contributions
- **Phi-4 (14B)** achieves performance competitive with or exceeding much larger models on reasoning benchmarks — outperforms Llama-3.1-70B and Qwen-2.5-72B on STEM despite 5× fewer parameters
- First model to **substantially surpass its teacher model (GPT-4)** on STEM QA, proving synthetic data goes beyond simple distillation
- **50 broad synthetic dataset types** with ~400B tokens, each using different seeds and multi-stage prompting — the most comprehensive synthetic pretraining data effort documented
- **Pivotal Token Search (PTS)**: Novel DPO data selection method that identifies individual tokens where the model's decision most impacts answer correctness
- Detailed documentation of synthetic data generation techniques, training curriculum, and post-training

## Method
### Pretraining
- **Architecture**: 14B parameter decoder-only Transformer, closely following Phi-3-medium (RoPE, SwiGLU, GQA, tiktoken tokenizer with 100K vocab)
- **Data composition**: Synthetic data (~40%), filtered web data (~15%), academic/books/code data (~15%), "web rewrites" data (~15%), acquired datasets (~15%)
- **Single-phase training**: Unlike Phi-3's two-phase approach, Phi-4 uses a single phase with carefully designed data mixture
- **50+ synthetic dataset types**: Question-answer pairs, structured exercises, fill-in-the-middle, multi-step reasoning chains, agent trajectories — all seeded from diverse organic sources
- **Data mixture search**: Systematic search over token allocations from different sources, evaluated via ablation models
- **Midtraining**: Context extension from 4K → 16K tokens

### Post-training
1. **SFT**: Fine-tune on diverse high-quality data across math, coding, reasoning, conversation, safety
2. **DPO Stage 1**: Standard DPO with chosen/rejected pairs
3. **DPO Stage 2**: Pivotal Token Search — identify tokens where model decisions critically affect correctness, create targeted preference pairs
4. **Hallucination mitigation**: Specific SFT + DPO data teaching model to refuse when uncertain

### Pivotal Token Search (PTS)
- For each token in a generation, estimate impact on final answer correctness
- Identify "pivotal" tokens where correct/incorrect choice determines outcome
- Generate DPO pairs that differ at exactly these pivotal positions
- More targeted than random preference sampling

## Results
| Benchmark | Phi-4 (14B) | GPT-4o | Llama-3.1-70B | Qwen-2.5-72B |
|---|---|---|---|---|
| MMLU | 84.8 | 88.1 | 83.6 | 85.3 |
| GPQA | 56.1 | 53.6 | 46.7 | 49.0 |
| MATH | 80.4 | 76.6 | 64.2 | 80.0 |
| HumanEval | 82.6 | 90.6 | 80.5 | 86.6 |
| AMC 2024 (Nov) | 75/150 | 67/150 | — | — |

- Phi-4 beats GPT-4o on GPQA and MATH despite being ~14B vs. frontier scale
- Competitive with 70B+ models across the board

## Models Released
- **Phi-4** (14B): Released on Hugging Face under Microsoft Research License

## Connections
- **Builds on**: Phi-1 ("Textbooks Are All You Need"), Phi-3 (small model + data quality), [[sources/dpo]] (alignment), [[concepts/distillation]]
- **Key innovations**: [[concepts/synthetic-data]], Pivotal Token Search
- **Related**: [[sources/fineweb]] (data curation), [[sources/smollm2]] (data-centric small models)
- **Organizations**: [[entities/orgs/microsoft]]
- **Models**: [[entities/models/phi]]

## Citation
> Abdin et al., "Phi-4 Technical Report," arXiv:2412.08905, 2024.
> https://huggingface.co/papers/2412.08905
