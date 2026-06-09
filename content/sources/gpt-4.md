---
type: source
arxiv_id: "2303.08774"
title: "GPT-4 Technical Report"
authors: ["OpenAI"]
date: 2023-03-15
org: "OpenAI"
tags: [frontier-model, multimodal, 2023]
upvotes: 7
---

# GPT-4 Technical Report

> The technical report for **GPT-4**, a multimodal Transformer model that achieved **human-level performance** on professional and academic benchmarks — including passing the bar exam in the 90th percentile. The most influential proprietary LLM, serving as the primary benchmark for open-source models to target.

## Key Contributions
- **Multimodal input**: Accepts both text and images as input (first commercial multimodal LLM)
- **Human-level on professional exams**: 90th percentile on bar exam, 88th on LSAT, strong on USMLE
- **Post-training alignment**: Extensive RLHF for improved factuality and adherence to guidelines
- **Predictable scaling**: Developed methodology to predict GPT-4's performance from smaller models, enabling reliable scaling laws for capability forecasting

## Results (Selected)
| Exam / Benchmark | GPT-4 Score | Human Comparison |
|---|---|---|
| Bar Exam (Uniform) | ~90th percentile | Passes |
| LSAT | ~88th percentile | Passes |
| SAT Math | 700/800 | ~93rd percentile |
| GRE Quantitative | 163/170 | ~80th percentile |
| MMLU (5-shot) | 86.4% | Expert-level |
| HumanEval (0-shot) | 67.0% | — |
| HellaSwag (10-shot) | 95.3% | — |

## Impact on Open Source
GPT-4 became the **benchmark target** for the open-source community:
- **[[sources/deepseek-v3|DeepSeek-V3]]**: First open model approaching GPT-4-level performance
- **[[sources/qwen3|Qwen3]]**: Claims to match GPT-4o on reasoning tasks
- **[[sources/llama-3|Llama 3.1-405B]]**: Meta's attempt to match GPT-4-class performance openly
- **[[sources/phi-4|Phi-4]]**: Microsoft's synthetic-data approach to beat GPT-4 on specific benchmarks at 14B scale
- **GPT-4-as-judge**: Widely used to evaluate other models (AlpacaEval, MT-Bench)

## What the Report Doesn't Reveal
The report is notably sparse on technical details — a deliberate departure from OpenAI's earlier transparency:
- **No architecture details**: Model size, training data, and training compute are not disclosed
- **No data details**: Training corpus composition is not described
- **Safety focus**: Much of the report covers safety testing, red teaming, and RLHF alignment

This opacity helped catalyze the open-source movement: projects like [[entities/models/llama|LLaMA]], [[entities/models/falcon|Falcon]], and [[entities/models/bloom|BLOOM]] were explicitly motivated by the need for transparent, reproducible alternatives.

## Connections
- Org: [[entities/orgs/openai|OpenAI]]
- Succeeded by: GPT-4o (multimodal generation), GPT-4 Turbo (128K context)
- Open alternatives: [[sources/deepseek-v3]], [[sources/llama-3]], [[sources/qwen3]]
- Concepts: [[concepts/rlhf|RLHF]], [[concepts/multimodal-models|Multimodal Models]]

## Citation
> OpenAI, "GPT-4 Technical Report," arXiv:2303.08774, 2023.
