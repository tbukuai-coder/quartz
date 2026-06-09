---
type: source
arxiv_id: "2605.06652"
title: "When No Benchmark Exists: Validating Comparative LLM Safety Scoring Without Ground-Truth Labels"
authors: ["Sushant Gautam", "Finn Schwall", "Annika Willoch Olstad", "Fernando Vallecillos Ruiz", "Birk Torpmann-Hagen", "Sunniva Maria Stordal Bjørklund", "Leon Moonen", "Klas Pettersen", "Michael A. Riegler"]
date: 2026-05
tags: [safety, evaluation, llm-safety, benchmarkless-scoring, scenario-based-audit]
upvotes: 1
---

# When No Benchmark Exists: Validating Comparative LLM Safety Scoring Without Ground-Truth Labels

> Formalizes benchmarkless comparative safety scoring for LLMs, replacing ground-truth labels with scenario-based audits that measure responsiveness, variance dominance, and stability through an instrumental-validity chain.

## Key Contributions
- Formalizes the "benchmarkless comparative safety scoring" problem: comparing candidate LLMs for safety before a labeled benchmark exists
- Proposes the instrumental-validity chain as the contract under which scenario-based audits count as deployment evidence
- Scores are only valid under fixed scenario pack, rubric, auditor, judge, sampling configuration, and rerun budget
- Introduces AUROC-based comparison with variance decomposition into target-driven variance vs. auditor/judge artifacts
- Proposes local-first scoring instruments that avoid global aggregation bias

## Method
The paper develops a statistical framework for safety comparison without ground truth:
1. **Scenario pack**: Fixed set of safety scenarios to evaluate
2. **Rubric**: Structured evaluation criteria for each scenario
3. **Auditor + Judge**: Two roles — the auditor generates evaluations, the judge provides consistency checks
4. **Sampling configuration + rerun budget**: Fixed randomness budget for reproducibility
5. **AUROC analysis**: Treats the comparison as a ranking problem and uses AUROC to measure discriminative power
6. **Variance decomposition**: Separates target-driven variance (signal) from auditor/judge artifacts (noise)
7. **Local-first scoring**: Computes scores within scenario subgroups before aggregation to avoid global bias

## Results
- Provides a rigorous framework for safety comparison in settings where no ground-truth benchmark exists
- Variance decomposition reveals when comparisons are meaningful vs. dominated by judge/auditor noise

## Datasets Used
- Scenario-based safety evaluation datasets

## Models Released
- GitHub: https://github.com/kelkalot/simpleaudit (14 stars)

## Connections
- Related: [[sources/compliance-vs-sensibility]] — reasoning controllability and safety
- Related concept: [[concepts/llm-safety]], [[concepts/llm-evaluation]]
- Related: [[sources/shieldgemma]] — safety-focused model

## Citation
> Gautam et al., "When No Benchmark Exists: Validating Comparative LLM Safety Scoring Without Ground-Truth Labels," arXiv:2605.06652, 2026.
