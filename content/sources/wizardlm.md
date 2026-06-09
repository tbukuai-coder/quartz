---
type: source
arxiv_id: "2304.12244"
title: "WizardLM: Empowering Large Language Models to Follow Complex Instructions"
authors: ["Can Xu", "Qingfeng Sun", "Kai Zheng", "Xiubo Geng", "Pu Zhao", "Jiazhan Feng", "Chongyang Tao", "Daxin Jiang"]
date: 2023-04-24
org: "Microsoft"
tags: [synthetic-data, instruction-tuning, evol-instruct, sft, 2023]
upvotes: 14
---

# WizardLM / Evol-Instruct

> Uses LLMs to iteratively evolve simple instructions into complex ones — creating high-quality instruction data at scale without human annotation. The Evol-Instruct technique was adopted by WizardCoder, WizardMath, and many synthetic data pipelines. 9.5K+ GitHub stars.

## Key Contributions
- **Evol-Instruct**: Automated instruction complexity evolution using LLM rewriting — two mutation types:
  - **In-depth evolution**: Make instructions more specific, add constraints, increase reasoning steps, complicate input
  - **In-breadth evolution**: Create entirely new topics/domains from existing instructions
- **Complexity-aware training**: Models trained on evolved data handle complex instructions better than those trained on human-written data
- **LLaMA + Evol-Instruct = WizardLM**: Beats Alpaca and Vicuna on complex instruction benchmarks
- **Spawned a family**: WizardCoder (code), WizardMath (math) — same technique, domain-specific evolution

## Method
1. **Seed instructions**: Start with simple instructions (e.g., from Alpaca's 52K)
2. **Evolution loop**: For each instruction, randomly select a mutation:
   - Add constraints, increase reasoning steps, complicate input (in-depth)
   - Generate new topic/skill from the instruction (in-breadth)
3. **Quality filtering**: Use ChatGPT to evolve and filter — discard instructions that are too similar, unanswerable, or contain errors
4. **Response generation**: Generate responses to evolved instructions using ChatGPT
5. **Training**: SFT on LLaMA with 70K/196K evolved instruction-response pairs

## Results
- **WizardLM-7B**: Surpasses Alpaca (52K human-written) on complex instructions
- **Evol-Instruct V2 (196K)**: Improved diversity and complexity over V1 (70K)
- Human evaluation: WizardLM preferred over Alpaca on instructions requiring multi-step reasoning
- AlpacaEval: Competitive with larger models trained on human-written data

## Impact on the Ecosystem
Evol-Instruct became a **standard technique** for synthetic data generation:
- [[sources/magpie|Magpie]] builds on similar principles (LLM-generated instruction data)
- WizardCoder: Evol-Instruct for code → beats Code Llama on HumanEval
- WizardMath: Evol-Instruct for math → beats many larger models on GSM8K/MATH
- Widely cited pattern in synthetic data literature

## Connections
- Extends: [[sources/self-instruct|Self-Instruct]] (adds complexity evolution to bootstrapping)
- Related: [[sources/magpie|Magpie]] (alignment data synthesis), [[concepts/synthetic-data|Synthetic Data]]
- Concepts: [[concepts/instruction-tuning|Instruction Tuning]], [[concepts/synthetic-data|Synthetic Data]]

## Citation
> Xu et al., "WizardLM: Empowering Large Language Models to Follow Complex Instructions," arXiv:2304.12244, 2023.
