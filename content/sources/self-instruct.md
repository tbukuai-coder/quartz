---
type: source
arxiv_id: "2212.10560"
title: "Self-Instruct: Aligning Language Model with Self Generated Instructions"
authors: ["Yizhong Wang", "Yeganeh Kordi", "Swaroop Mishra", "et al."]
date: 2022-12-20
org: "University of Washington / AI2"
tags: [instruction-tuning, data-generation, foundational]
upvotes: 9
---

# Self-Instruct: Aligning Language Models with Self-Generated Instructions

> Introduced a framework for **bootstrapping instruction data from the model itself**, producing 52K instruction-response pairs that significantly improve instruction-following, nearly matching InstructGPT.

## Key Contributions
- Proposed a **self-bootstrapping pipeline** for generating instruction-following data
- Starting from 175 seed tasks, generated **52K diverse instruction-response pairs** using GPT-3
- Showed that fine-tuning on self-generated data nearly matches human-written instruction data
- Demonstrated that instruction-tuning does not require expensive human annotation
- Directly inspired **Alpaca** (Stanford), which used the same approach with GPT-3.5/4

## Method
1. Start with a **seed set** of 175 human-written tasks (instruction + input/output)
2. **Generate new instructions**: Prompt GPT-3 with 8 examples from the seed set to generate new instructions
3. **Classify**: Determine if the instruction requires an input or is self-contained
4. **Generate instances**: Use GPT-3 to generate input-output pairs for each instruction
5. **Filter**: Remove low-quality, duplicate, or too-similar instructions
6. Repeat: new instructions feed back into the pool

After iterations, produces ~52K diverse instructions covering classification, generation, rewriting, Q&A, brainstorming, etc.

## Results
- GPT-3 + Self-Instruct achieves **33% absolute improvement** over vanilla GPT-3 on Super-NaturalInstructions
- Nearly matches InstructGPT (text-davinci-001) on human evaluation
- Generated dataset covers broad task diversity

## Connections
- **Influenced**: Alpaca, [[sources/zephyr]] (distilled data from stronger models), the entire synthetic instruction data movement
- **Key concepts**: [[concepts/instruction-tuning]], [[concepts/distillation]]
- **Related**: [[sources/constitutional-ai]] (AI-generated training signals)

## Citation
> Wang et al., "Self-Instruct: Aligning Language Model with Self Generated Instructions," arXiv:2212.10560, 2022.
> https://huggingface.co/papers/2212.10560
