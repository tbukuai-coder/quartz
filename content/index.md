# 🗂️ Index — HF Papers Wiki

> Master catalog of all wiki pages. Read this first to navigate the wiki.

Last updated: 2026-06-02 (Batch 31 complete — 14 papers)

---

## 📖 Overview

- [[overview]] — High-level synthesis of the Hugging Face open-source ML ecosystem

---

## 📄 Source Pages (Papers) — 270 papers ingested

*(For the complete listing of all 145 papers from batches 1-18, see previous index versions. Below shows key additions from batches 19–31.)*

### Batch 30: Multi-Agent Worlds, Token Credit, Skill Optimization, Autonomous Research, Olympiad Reasoning (11 papers)
| Paper | Year | Key Contribution | Page |
|---|---|---|---|
| **Gamma-World** | 2026 | Multi-agent world modeling, Simplex Rotary Encoding, 24 FPS (410⬆️) | [[sources/gamma-world]] |
| **CiteVQA** | 2026 | Document VQA evidence attribution benchmark (269⬆️) | [[sources/citevqa]] |
| **SkillOpt** | 2026 | Text-space optimizer for agent skills, +39.0 gains (212⬆️) | [[sources/skillopt]] |
| **DelTA** | 2026 | Discriminator view of RLVR, token credit assignment (204⬆️) | [[sources/delta-token-credit]] |
| **Anti-Self-Distillation** | 2026 | PMI reversal of self-distillation for reasoning (195⬆️) | [[sources/anti-self-distillation]] |
| **AutoResearchClaw** | 2026 | Multi-agent autonomous research, 13K⭐ (185⬆️) | [[sources/autoresearchclaw]] |
| **SU-01** | 2026 | IMO/IPhO gold-medal via unified RL recipe (159⬆️) | [[sources/su-01-olympiad]] |
| **PhysBrain 1.0** | 2026 | VLA with physical commonsense (143⬆️) | [[sources/physbrain]] |
| **SDAR** | 2026 | Self-distilled agentic RL, sigmoid-gated guidance (111⬆️) | [[sources/sdar]] |
| **Qwen-Image-2.0** | 2026 | Omni image gen via Qwen3-VL + MMDiT (110⬆️) | [[sources/qwen-image-2]] |
| **Darwin Family** | 2026 | Evolutionary merging, cross-architecture breeding (60⬆️) | [[sources/darwin-family]] |

### Batch 31: Infrastructure, Agent Skills Governance, Video Distillation, World Models, Non-Transformer, Speech, Grounding (14 papers)
| Paper | Year | Key Contribution | Page |
|---|---|---|---|
| **MinT** | 2026 | Managed infrastructure for millions of LoRA policies (219⬆️) | [[sources/mint-infrastructure]] |
| **Code as Agent Harness** | 2026 | Code as unified substrate for agent capabilities (211⬆️) | [[sources/code-as-agent-harness]] |
| **Video2GUI** | 2026 | GUI trajectories from internet video for agent pretraining (145⬆️) | [[sources/video2gui]] |
| **MulTaBench** | 2026 | Multimodal tabular learning benchmark (140⬆️) | [[sources/multabench]] |
| **Mega-ASR** | 2026 | Robust ASR via compound-data + progressive optimization (131⬆️) | [[sources/mega-asr]] |
| **LocateAnything** | 2026 | Parallel Box Decoding for fast VL grounding (130⬆️) | [[sources/locateanything]] |
| **SkillsVote** | 2026 | Lifecycle governance for agent skill ecosystems (126⬆️) | [[sources/skillsvote]] |
| **LongLive-2.0** | 2026 | NVFP4 parallel infra for minute-scale video, 2.1K⭐ (112⬆️) | [[sources/longlive-2]] |
| **AnyFlow** | 2026 | Any-step video via flow map distillation, 354⭐ (101⬆️) | [[sources/anyflow]] |
| **Causal Forcing++** | 2026 | Frame-wise 1-2 step AR for real-time video (92⬆️) | [[sources/causal-forcing-pp]] |
| **MIGA** | 2026 | Train-free infinite-frame long video generation (91⬆️) | [[sources/miga-long-video]] |
| **HRM-Text** | 2026 | Hierarchical Recurrent Model, non-Transformer, 987⭐ (90⬆️) | [[sources/hrm-text]] |
| **SANA-WM** | 2026 | 2.6B world model with hybrid GDN + softmax attention (84⬆️) | [[sources/sana-wm]] |
| **Lance** | 2026 | Unified multimodal via dual-stream MoE, 1K⭐ (78⬆️) | [[sources/lance]] |

---

### Thematic Indexes (Cross-Batch)

### Reasoning & RL
| Paper | Key Contribution | Page |
|---|---|---|
| DeepSeek-R1 | Pure RL → emergent CoT | [[sources/deepseek-r1]] |
| GRPO variants | LoPE, Balanced Agg, ResRL, DelTA | [[sources/nonsense-helps-lope]] [[sources/balanced-aggregation-grpo]] [[sources/resrl]] [[sources/delta-token-credit]] |
| Anti-Self-Distillation | PMI reversal for reasoning RL | [[sources/anti-self-distillation]] |
| SU-01 | Gold-medal olympiad reasoning | [[sources/su-01-olympiad]] |
| ScaleLogic | Power-law scaling for reasoning depth | [[sources/scalelogic]] |

### Agents & Skills
| Paper | Key Contribution | Page |
|---|---|---|
| SkillOpt | Text-space skill optimizer | [[sources/skillopt]] |
| Skill1 | Unified skill evolution via shared RL | [[sources/skill1]] |
| SkillOS | RL-based skill curation | [[sources/skillos]] |
| SkillsVote | Lifecycle governance for skill ecosystems | [[sources/skillsvote]] |
| Code as Agent Harness | Code as unified agent substrate | [[sources/code-as-agent-harness]] |
| AutoResearchClaw | Multi-agent autonomous research | [[sources/autoresearchclaw]] |
| Video2GUI | GUI pretraining from internet video | [[sources/video2gui]] |
| SDAR | Self-distilled agentic RL | [[sources/sdar]] |

### Video Generation & World Models
| Paper | Key Contribution | Page |
|---|---|---|
| Gamma-World | Multi-agent interactive world model | [[sources/gamma-world]] |
| SANA-WM | Efficient hybrid-attention world model | [[sources/sana-wm]] |
| LongLive-2.0 | NVFP4 parallel long-video infra | [[sources/longlive-2]] |
| AnyFlow | Any-step flow map distillation | [[sources/anyflow]] |
| Causal Forcing++ | Frame-wise real-time generation | [[sources/causal-forcing-pp]] |
| MIGA | Train-free infinite-frame generation | [[sources/miga-long-video]] |
| Stream-T1 | Active test-time scaling for video | [[sources/stream-t1]] |

### Infrastructure & Architecture
| Paper | Key Contribution | Page |
|---|---|---|
| MinT | Managed LoRA training/serving at scale | [[sources/mint-infrastructure]] |
| HRM-Text | Non-Transformer hierarchical recurrence | [[sources/hrm-text]] |
| RoundPipe | Consumer GPU pipeline parallelism | [[sources/roundpipe]] |
| Prima.cpp | Distributed home inference | [[sources/prima-cpp]] |

### Evaluation & Benchmarks
| Paper | Key Contribution | Page |
|---|---|---|
| CiteVQA | Document VQA evidence attribution | [[sources/citevqa]] |
| MulTaBench | Multimodal tabular learning | [[sources/multabench]] |
| LocateAnything | Parallel Box Decoding for grounding | [[sources/locateanything]] |
| Mega-ASR | Robust real-world speech recognition | [[sources/mega-asr]] |

---

## 🏗️ Entity Pages — 20 models, 12 datasets, 22 orgs

## 💡 Concept Pages — 54 concepts

## 📊 Comparisons — 15

| Comparison | Page |
|---|---|
| Open Model Families (2023–2025) | [[comparisons/open-model-families]] |
| Alignment Methods: RLHF vs DPO vs GRPO | [[comparisons/alignment-methods]] |
| Reasoning Models | [[comparisons/reasoning-models]] |
| Pretraining Data | [[comparisons/pretraining-data]] |
| Vision-Language Models | [[comparisons/vision-language-models]] |
| Open-Science vs Open-Weight | [[comparisons/open-science-vs-open-weight]] |
| Small Language Models | [[comparisons/small-language-models]] |
| Inference Engines | [[comparisons/inference-engines]] |
| Embedding Models | [[comparisons/embedding-models]] |
| MoE Architectures | [[comparisons/moe-architectures]] |
| Code Models & Agents | [[comparisons/code-models-agents]] |
| Diffusion Architectures | [[comparisons/diffusion-architectures]] |
| Context Extension Methods | [[comparisons/context-extension-methods]] |
| Quantization Landscape | [[comparisons/quantization-landscape]] |
| RL Reasoning Methods | [[comparisons/rl-reasoning-methods]] |

---

*This index is updated on every ingest and maintenance pass. 270 papers, 20 models, 12 datasets, 22 orgs, 54 concepts, 15 comparisons = 397 pages total.*
