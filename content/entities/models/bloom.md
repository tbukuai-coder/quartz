---
type: entity
category: model
tags: [open-models, bigscience, multilingual, collaborative, foundational]
---

# BLOOM

> The first **176B-parameter open-access multilingual** language model — created by a collaboration of **hundreds of researchers** in the BigScience workshop. Trained on the **ROOTS corpus** covering **46 natural languages and 13 programming languages**, BLOOM demonstrated that large-scale AI can be developed through open, international collaboration.

## Overview
BLOOM (BigScience Large Open-science Open-access Multilingual Language Model) was a landmark project in AI democratization. Unlike models from well-funded corporate labs, BLOOM was built through an open research collaboration organized by Hugging Face, trained on the French government-funded Jean Zay supercomputer. The project involved 1,000+ researchers from 60+ countries and 250+ institutions, making it the largest-ever collaborative effort to build an LLM. BLOOM proved that frontier-scale models could be developed through international, values-driven collaboration — though its technical performance was eventually surpassed by later models like LLaMA.

## Model Family

| Model | Params | Layers | Hidden Dim | Attention Heads |
|---|---|---|---|---|
| BLOOM-560M | 559M | 24 | 1024 | 16 |
| BLOOM-1.1B | 1.07B | 24 | 1536 | 16 |
| BLOOM-1.7B | 1.72B | 24 | 2048 | 16 |
| BLOOM-3B | 3.0B | 30 | 2560 | 32 |
| BLOOM-7.1B | 7.07B | 30 | 4096 | 32 |
| **BLOOM** | **176B** | **70** | **14336** | **112** |

Post-trained variant: **BLOOMZ** — multitask-prompted finetuning on xP3 (crosslingual prompt collection), significantly improving zero-shot task generalization.

## Architecture
BLOOM deviates from the now-standard "LLaMA template" in several ways, reflecting the state of the art in 2022:
- **Decoder-only Transformer** (causal LM)
- **ALiBi positional embeddings** (not RoPE) — chosen for extrapolation to longer sequences
- **Embedding LayerNorm**: Additional LayerNorm after the embedding layer (found to improve training stability at 104B+ scale)
- **float16 precision** (560M–7.1B), **bfloat16** (176B)
- **No parallel attention/MLP** (sequential, standard Transformer)
- **Tokenizer**: Byte-level BPE with 250,680 vocabulary — designed for multilingual fairness (fertility analysis across languages)

## Training Data: ROOTS Corpus
The ROOTS (Responsible Open-science Open-collaboration Text Sources) corpus is a unique dataset:
- **1.61 TB of text** across **46 natural languages** and **13 programming languages** (59 total)
- **498 component datasets** curated by language-specific working groups
- Sources: OSCAR (web), Wikipedia, academic papers, books, code, and institutional sources
- **Explicit language governance**: Each language community had representatives involved in data selection
- **Data documentation**: Detailed provenance and consent tracking

### Language Distribution (Top)
| Language | % of Tokens | Notes |
|---|---|---|
| English | 30.0% | Largest single language |
| Simplified Chinese | 16.2% | |
| French | 12.9% | (Host country) |
| Spanish | 10.8% | |
| Code (13 langs) | 10.6% | Python, C++, Java, etc. |
| Arabic | 4.6% | |
| Other (40 langs) | 14.9% | Including Catalan, Basque, Swahili, etc. |

## Benchmarks
| Task | BLOOM-176B | OPT-175B | GPT-3 175B |
|---|---|---|---|
| SuperGLUE (0-shot) | Competitive | Competitive | — |
| WMT (en→fr, 1-shot) | 38.0 BLEU | 31.4 BLEU | — |
| HumanEval (pass@1) | 15.5% | 15.6% | — |
| MMLU (5-shot) | ~39% | ~35% | ~43% |

BLOOM showed particular strength in multilingual tasks, especially machine translation, where it significantly outperformed monolingual models like OPT.

## Significance
1. **Democratization**: Proved frontier-scale models can be built through open, international collaboration rather than only by well-funded corporate labs
2. **Multilingual commitment**: First 100B+ model designed from the ground up for multilingual support with explicit linguistic fairness considerations
3. **Responsible AI License (RAIL)**: Introduced the RAIL license model — permissive with behavioral-use restrictions — adopted and adapted by later models (Llama, Stability AI)
4. **Community process**: Established governance patterns for collaborative AI development (working groups, ethics review, transparent documentation)
5. **Training infrastructure**: Demonstrated successful training on government-funded HPC (Jean Zay, 384 A100 80GB GPUs)

## Limitations
- Performance was below GPT-3/PaLM at similar scale, partly due to architectural choices (ALiBi vs. RoPE, tokenizer) and data constraints
- Quickly surpassed by LLaMA (Feb 2023) which was smaller, faster, and more performant
- ROOTS corpus not fully open (some components have access restrictions)

## Related Papers
- [[sources/bloom]] — BLOOM paper (BigScience Workshop)
- [[sources/bert]] — BERT (foundational encoder model by Google)

## See Also
- [[entities/orgs/huggingface]] — Hugging Face (BigScience organizer)
- [[entities/models/llama]] — LLaMA (succeeded BLOOM as dominant open model)
- [[entities/models/falcon]] — Falcon (another non-US open model project)
- [[concepts/multilingual-models]] — Multilingual model design
- [[concepts/tokenization]] — Tokenizer design for multilingual fairness
- [[concepts/pre-training]] — Pre-training at scale
- [[comparisons/open-model-families]] — Model family comparison
