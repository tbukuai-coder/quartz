---
type: source
arxiv_id: "2605.04330"
title: "The Scaling Properties of Implicit Deductive Reasoning in Transformers"
authors: ["Enrico Vompa", "Tanel Tammet"]
date: 2026-05
tags: [transformer-architecture, reasoning, horn-clauses, chain-of-thought, deductive-reasoning, bidirectional-attention]
upvotes: 1
---

# The Scaling Properties of Implicit Deductive Reasoning in Transformers

> Deep Transformers with bidirectional prefix masking exhibit implicit deductive reasoning capabilities comparable to explicit chain-of-thought methods across various graph structures and problem sizes, though CoT remains necessary for depth extrapolation.

## Key Contributions
- Investigates implicit deductive reasoning over Horn clauses in depth-bounded Transformers
- Systematically decorrelates provability from spurious features to enable clean measurement
- Enforces algorithmic alignment between the model architecture and the reasoning task
- Finds that in sufficiently deep models with bidirectional prefix masking, implicit reasoning approaches explicit CoT performance
- However, explicit chain-of-thought remains necessary for depth extrapolation (generalizing to deeper reasoning chains than seen in training)

## Method
The experimental setup:
1. **Horn clause reasoning**: Uses propositional Horn clauses as a controlled testbed for deductive reasoning
2. **Depth-bounded Transformers**: Models with limited depth to study scaling properties
3. **Bidirectional prefix mask**: Allows the model to attend to all previous tokens in the reasoning chain (not just left-to-right)
4. **Algorithmic alignment**: Careful task design that matches the model's inductive biases to the reasoning structure
5. **Graph topologies**: Tests on various graph structures (trees, chains, DAGs) and problem widths

## Results
- Implicit reasoning in deep Transformers with bidirectional masking approaches explicit CoT performance
- Performance holds across diverse graph topologies and problem sizes
- Explicit CoT is still needed for depth extrapolation (reasoning beyond training depth)
- Algorithmic alignment is critical — without it, models exploit spurious features

## Datasets Used
- Synthetic Horn clause reasoning datasets with controlled graph structures

## Models Released
- None explicitly mentioned

## Connections
- Related: [[sources/scaling-test-time-compute]] — test-time scaling for reasoning
- Related: [[sources/deepseek-r1]] — emergent reasoning from RL
- Related: [[sources/lets-verify-step-by-step]] — process reward models for reasoning
- Related concept: [[concepts/chain-of-thought]], [[concepts/test-time-compute]]

## Citation
> Vompa et al., "The Scaling Properties of Implicit Deductive Reasoning in Transformers," arXiv:2605.04330, 2026.
