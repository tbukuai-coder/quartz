---
type: source
arxiv_id: "2511.22570"
title: "DeepSeekMath-V2: Towards Self-Verifiable Mathematical Reasoning"
authors: ["Zhihong Shao", "Yuxiang Luo", "Chengda Lu"]
date: 2025-11-27
org: "DeepSeek"
tags: [reasoning, math, theorem-proving, rl, 2025]
upvotes: 93
---

# DeepSeekMath-V2

> Self-verifying math reasoning model that incentivizes rigorous step-by-step derivations and achieves high scores on IMO, CMO, and Putnam — moving beyond just correct final answers.

## Key Contributions
- Introduced **self-verification** for mathematical reasoning: the model proves its own answers are correct via theorem-proving capabilities
- Moved beyond **final-answer accuracy** — incentivizes rigorous step-by-step derivations that can be formally verified
- Achieves strong performance on **IMO, CMO, and Putnam** competition problems
- Combines **proof generation** with a **reward model** trained on verification outcomes
- Scales verification compute: more verification attempts → higher confidence in answers

## Method
Two-stage approach:
1. **Solution generation**: Model generates mathematical solutions with detailed step-by-step reasoning
2. **Self-verification**: A theorem-proving component attempts to formally verify the solution steps
3. **RL with verification reward**: Model is trained with RL where rewards come from successful verification, not just correct final answers

This incentivizes the model to produce solutions that are not only correct but also rigorously derivable — a fundamentally different objective from typical reward-based RL.

## Results
- **IMO**: Strong multi-problem performance
- **CMO (Chinese Mathematical Olympiad)**: Competitive scores
- **Putnam**: Significant improvement over prior math models
- **AIME**: Near-saturation performance
- Self-verification reliably identifies incorrect reasoning steps

## Connections
- **Builds on**: [[sources/deepseekmath|DeepSeekMath/GRPO]], [[sources/deepseek-r1|DeepSeek-R1]]
- **Related**: [[sources/deepseek-prover-v2|DeepSeek-Prover-V2]] (formal theorem proving)
- **Part of**: [[entities/models/deepseek|DeepSeek]] family
- **Related concepts**: [[concepts/grpo|GRPO]], [[concepts/process-reward-models|Process Reward Models]], [[concepts/chain-of-thought|Chain-of-Thought]]

## Citation
> Shao et al., "DeepSeekMath-V2: Towards Self-Verifiable Mathematical Reasoning," arXiv:2511.22570, 2025.
