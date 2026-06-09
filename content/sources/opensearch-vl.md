---
type: source
arxiv_id: "2605.05185"
title: "OpenSearch-VL: An Open Recipe for Frontier Multimodal Search Agents"
authors:
  - Shuang Chen
  - Kaituo Feng
  - Hangting Chen
  - Wenxuan Huang
  - Dasen Dai
  - Quanxin Shou
  - Yunlong Lin
  - Xiangyu Yue
  - Shenghua Gao
  - Tianyu Pang
venue: arXiv
year: 2026
month: 5
date: "2026-05"
upvotes: 86
tags:
  - agents
  - multimodal-search
  - reinforcement-learning
  - grpo
  - tool-use
  - open-science
github: https://github.com/shawn0728/OpenSearch-VL
stars: 99
---

# OpenSearch-VL: An Open Recipe for Frontier Multimodal Search Agents

## One-Line Summary

Fully open-source training recipe for multimodal deep search agents, combining Wikipedia-based multi-hop VQA data curation, diverse visual tool environments, and fatal-aware GRPO to achieve frontier performance across 7 benchmarks.

## Key Contributions

1. **Fully open recipe** — Releases training data (SearchVL-SFT-36k + SearchVL-RL-8k), code, and models for reproducible multimodal search agent research.
2. **Wikipedia multi-hop VQA pipeline** — Samples constrained random walks over the Wikipedia hyperlink graph (hops ∈ {2,3,4}), converts paths into fuzzy visual questions via entity rewriting and source-anchor visual grounding. Prevents single-hop retrieval shortcuts.
3. **Diverse tool environment** — Beyond search: OCR, cropping, sharpening, super-resolution, and perspective correction for handling imperfect real-world visual inputs.
4. **Fatal-aware Multi-Turn GRPO** — Introduces fatal-aware token masking (removes invalid post-failure suffixes) and one-sided advantage clamping (preserves useful pre-failure reasoning) for long-horizon multimodal tool use.
5. **Composite multi-turn reward** — Balances format correctness ($r_{\text{fmt}}$), answer accuracy ($r_{\text{acc}}$), and query quality ($r_{\text{query}}$) with $\alpha=0.8$.

## Method

### Data Curation (3 stages)

**Stage 1: High-Quality VQA Construction**
- Wikipedia as directed graph $\mathcal{G}=(\mathcal{V}, \mathcal{E})$
- Constrained random walk from seed $v_0$ with length $h \in \{2,3,4\}$
- Nodes assigned functional roles: anchor (visual entry), bridge (intermediate entities with fuzzified names), answer (target attribute)
- **Fuzzy Entity Rewriting**: Progressive replacement of entity names with relational descriptors; verified via LLM uniqueness evaluator ensuring answer invariance, uniqueness, and non-leakage
- **Source-Anchor Visual Grounding**: Retrieve representative image of anchor $v_0$ from Wikimedia Commons, replace $v_0$ with visual referring expression in final question

**Stage 2: Filtering & Enhancement**
- Merged with LiveVQA, FVQA, WebQA for coverage
- Two-stage difficulty filter (frozen Qwen3-VL-32B): discard answerable-without-tools, then discard solvable-with-single-ImageSearch
- 10% controlled degradation subset (blur, downsampling, perspective distortion) paired with enhancement tools to induce "think-with-image" behavior

**Stage 3: Multi-Turn Trajectory Synthesis**
- Expert trajectories rolled out with Claude Opus 4.6 in real tool environment
- Rejection sampling with answer-correctness + process-level judges

### Training

**SFT**: 36,592 multi-turn expert trajectories on Qwen3-VL variants (8B, 30B-A3B, 32B). 2 days on 256 H20s (8B), 4 days (30B-A3B).

**RL**: Fatal-aware GRPO on 8K examples, ~200 steps over 10 days on 64 H20s.

**Fatal-Aware Design**:
- Fatal step index $f_i$: earliest step with K=3 consecutive tool-execution errors
- Token mask zeros out all tokens after fatal step: $M(y_{i,t}) = M_{\text{gen}}(y_{i,t}) \cdot \mathbb{1}[s(t) < f_i]$
- One-sided advantage clamping preserves valid pre-failure reasoning

## Results

**OpenSearch-VL-32B** achieves **63.7 average** across 7 benchmarks, outperforming:
- Direct-reasoning: Gemini-2.5-Pro (46.0), GPT-5 (45.1)
- RAG workflows: GPT-5+RAG (53.6)
- Agentic baselines: Qwen3-VL-32B agentic (48.0), WebWatcher-32B (—)

| Benchmark | OpenSearch-VL-32B | Qwen3-VL-32B Baseline | Gain |
|---|---|---|---|
| SimpleVQA | 76.2 | 58.7 | +17.5 |
| VDR | 33.8 | 23.1 | +10.7 |
| MMSearch | 72.3 | 53.9 | +18.4 |
| LiveVQA | 70.5 | 45.5 | +25.0 |
| BrowseComp-VL | 43.8 | 35.1 | +8.7 |
| FVQA | 74.7 | 61.2 | +13.5 |
| InfoSeek | 74.8 | 58.5 | +16.3 |

**Scaling**: Effective from 8B (56.6 avg) to 30B-A3B (61.6) to 32B (63.7).

**Ablations**:
- Removing source-anchor grounding: -11.5 points
- Removing fuzzy entity rewriting: -10.3 points  
- Removing staged filtering: -8.2 points
- Fatal masking + one-sided clamp vs vanilla GRPO: +4.2 points

## Connections

- **Data Synthesis**: Wikipedia path sampling with fuzzy rewriting extends [[sources/web2bigtable|Web2BigTable]]'s bi-level multi-agent search to the visual domain. Both prevent shortcut retrieval.
- **Fatal-Aware RL**: Builds on [[sources/multi-turn-agent-rl|Multi-Turn Agent RL]]'s turn-level credit assignment and [[sources/a2tgpo-agentic|A²TGPO]]'s adaptive turn-level clipping, but specifically addresses cascading tool failures in multimodal settings.
- **Tool Environment**: Visual enhancement tools (OCR, crop, sharpen, SR, perspective correction) complement [[sources/grit|GRIT]]'s visual reasoning chains and [[sources/oscar-vlm|OSCAR]]'s hallucination calibration.
- **Open Recipe**: Follows [[sources/agent-native-research-artifact|Ara]] protocol and [[sources/intern-atlas|Intern-Atlas]] mission for agent-executable research artifacts.
- **GRPO Foundation**: Extends [[concepts/grpo|GRPO]] to multimodal search with composite rewards and fatal-aware masking.

## Citation

```bibtex
@article{chen2026opensearchvl,
  title={OpenSearch-VL: An Open Recipe for Frontier Multimodal Search Agents},
  author={Chen, Shuang and Feng, Kaituo and Chen, Hangting and Huang, Wenxuan and Dai, Dasen and Shou, Quanxin and Lin, Yunlong and Yue, Xiangyu and Gao, Shenghua and Pang, Tianyu},
  journal={arXiv preprint arXiv:2605.05185},
  year={2026}
}
```

---
*Ingested in Batch 26 (2026-05-05)* | [[index]] | [[concepts/agents]] | [[concepts/grpo]] | [[comparisons/vision-language-models]]