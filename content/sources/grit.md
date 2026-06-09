---
type: source
arxiv_id: "2505.15879"
title: "GRIT: Teaching MLLMs to Think with Images"
authors: ["Yue Fan", "Xuehai He", "Diji Yang", "Kaizhi Zheng", "Ching-Chen Kuo", "Yuting Zheng", "Sravana Jyothi Narayanaraju", "Xinze Guan", "Xin Eric Wang"]
date: 2025-05-24
org: "UC Santa Barbara / UC San Diego / Amazon"
tags: [multimodal, vlm, reasoning, rl, grpo, grounding, visual-reasoning, 2025]
upvotes: 13
---

# GRIT: Teaching MLLMs to Think with Images

> A grounded reasoning method that teaches multimodal LLMs to generate reasoning chains interleaving natural language with bounding box coordinates — trained with only 20 image-question-answer triplets via GRPO-GR reinforcement learning.

## Key Contributions
- **Grounded reasoning paradigm**: MLLMs generate reasoning chains that freely mix natural language with bounding box coordinates, explicitly grounding visual reasoning in the input image
- **GRPO-GR algorithm**: A GRPO variant with novel format rewards for both reasoning structure and grounding quality — no need for reasoning chain or bounding box annotations
- **Extreme data efficiency**: Trains Qwen 2.5-VL and InternVL 3 with only 20 image-question-answer triplets from existing VQA datasets
- **Unified capabilities**: Trained models preserve versatility — handling both VQA and grounding-heavy referring expression comprehension
- **High correlation**: Generated bounding boxes show strong alignment with accompanying reasoning text

## Method

### Grounded Reasoning Format
The model generates reasoning chains in this format:
```
<think>
[Natural language reasoning with bounding box coordinates]
(e.g., "The bounding box coordinates for the truck are approximately (0, 209, 488, 364)")
</think>
<rethink>
[Reflection on previous reasoning]
</rethink>
<answer>
[Final answer]
</answer>
```

Bounding boxes are generated as text tokens and serve to indicate which visual regions the model is consulting. After generating coordinates, no additional pixel inputs are provided — the model comprehends visual information from its understanding of the original image.

### GRPO-GR: GRPO for Grounded Reasoning
Three reward components:
1. **Answer accuracy**: GPT-as-judge evaluation of answer correctness
2. **Format reward**: Checks for syntactically valid bounding boxes and proper think/answer structure
3. **Grounding format reward**: Rewards inclusion of bounding box coordinates in reasoning

**Key insight**: The rewards only constrain format, not content — enabling data-efficient learning without human-annotated reasoning chains or bounding box labels.

## Results

### Qwen 2.5-VL 3B Results

| Method | VSR (ACC/GIoU) | TallyQA (ACC/GIoU) | GQA (ACC/GIoU) | MathVista (ACC) |
|---|---|---|---|---|
| Direct Query | 49.5 / 0.00 | 40.8 / 0.00 | 55.4 / 0.00 | 58.5 |
| Chain-of-Thought | 37.5 / 0.122 | 33.2 / 0.113 | 39.5 / 0.269 | 33.0 |
| Few-shot SFT | 59.7 / 0.216 | 44.5 / 0.284 | 64.6 / 0.475 | 45.0 |
| **GRIT** | **72.9 / 0.325** | **47.8 / 0.447** | **62.8 / 0.485** | **59.8** |

Key findings:
- GRIT unifies grounding and reasoning abilities that were disconnected in base MLLMs
- High correlation between referenced image regions and accompanying reasoning text
- Bounding box generation boosts subsequent reasoning attention to relevant visual regions
- Zero-shot baselines struggle — they generate either only text OR only boxes, but not both coherently
- Few-shot SFT learns surface form mimicry; GRIT develops deeply integrated reasoning

## Datasets Used
- **VSR** — Visual Spatial Reasoning (20 training triplets)
- **TallyQA** — Counting VQA (20 training triplets)
- Testing: GQA, MathVista, MME, OVDEval

## Models Used
- Qwen 2.5-VL (3B) — Base multimodal model
- InternVL 3 (2B) — Base multimodal model

## Connections
- Builds on: [[sources/qwen25-vl|Qwen2.5-VL]] (base MLLM), [[sources/internvl-3|InternVL 3]] (base MLLM), [[sources/deepseek-r1|DeepSeek-R1]] (GRPO reasoning paradigm)
- Cited by / Influenced: Pioneers visual reasoning chains — extends textual CoT to multimodal domain
- Related concepts: [[concepts/vision-language-models|Vision-Language Models]], [[concepts/chain-of-thought|Chain-of-Thought]], [[concepts/grpo|GRPO]]
- Related papers: [[sources/cambrian|Cambrian-1]] (vision-centric MLLM), [[sources/qwen25-vl|Qwen2.5-VL]] (native dynamic ViT)
- GitHub: [eric-ai-lab/GRIT](https://github.com/eric-ai-lab/GRIT) (185 ⭐)

## Citation
> Fan et al., "GRIT: Teaching MLLMs to Think with Images," arXiv:2505.15879, 2025.
