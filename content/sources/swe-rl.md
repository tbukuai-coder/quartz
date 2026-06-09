---
type: source
arxiv_id: "2502.18449"
title: "SWE-RL: Advancing LLM Reasoning via Reinforcement Learning on Open Software Evolution"
authors: ["Yuxiang Wei", "Olivier Duchenne", "Jade Copet", "Quentin Carbonneaux", "Lingming Zhang"]
date: 2025-02-25
org: "Meta AI / Various"
tags: [reasoning, rl, code, agents, 2025]
upvotes: 75
---

# SWE-RL

> First approach to scale RL-based reasoning for real-world software engineering — trains on open-source git evolution data and achieves SOTA on SWE-bench while generalizing to math and language tasks.

## Key Contributions
- **First RL approach for real-world software engineering** reasoning — extending beyond the typical math/code competition setting
- Uses **open-source software evolution data** (git commits, PRs) as training signal — massive natural source of code reasoning examples
- Employs a **lightweight rule-based reward** (similarity between model output and ground-truth patch)
- Achieves **SOTA on SWE-bench Verified** when applied to Llama 3 models
- **Generalizes beyond code**: RL on software engineering data improves math and general language understanding

## Method
1. **Data**: Collect (problem description, solution) pairs from open-source git history — natural "reasoning traces" from real developers
2. **Reward**: Simple similarity score between generated patch and ground-truth commit
3. **RL training**: Standard GRPO/PPO on Llama 3 base models
4. **Evaluation**: SWE-bench Verified (real GitHub issues) + coding benchmarks + math + general reasoning

Key insight: Real-world software engineering provides naturally complex reasoning tasks with verifiable outcomes — a rich RL training signal.

## Results
- **SWE-bench Verified**: New SOTA solve rate for open models
- **Function coding (HumanEval)**: Improved alongside SWE-bench
- **Math (GSM8K, MATH)**: Surprising improvement from code RL
- **General language (MMLU)**: Maintained or slightly improved
- **Transfer**: Software engineering RL generalizes to non-code reasoning

## Models Released
- SWE-RL models based on Llama 3 (Meta, open)

## Connections
- **Builds on**: [[sources/deepseek-r1|DeepSeek-R1]] (RL for reasoning), [[sources/llama-3|Llama 3]]
- **Related**: [[sources/swe-agent|SWE-agent]] (agent approach), [[sources/codeact|CodeAct]]
- **Org**: [[entities/orgs/meta|Meta AI]]
- **Related concepts**: [[concepts/grpo|GRPO]], [[concepts/agents|Agents]], [[concepts/rlhf|RLHF]]
- **Key insight**: RL on real-world tasks generalizes better than RL on synthetic problems

## Citation
> Wei et al., "SWE-RL: Advancing LLM Reasoning via Reinforcement Learning on Open Software Evolution," arXiv:2502.18449, 2025.
