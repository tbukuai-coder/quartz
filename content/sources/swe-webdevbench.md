---
type: source
arxiv_id: "2605.04637"
title: "SWE-WebDevBench: Evaluating Coding Agent Application Platforms as Virtual Software Agencies"
authors: ["Siddhant Saxena", "Nilesh Trivedi", "Vinayaka Jyothi"]
venue: "arXiv preprint"
year: 2026
date: "2026-05"
org: "SnowMountain AI"
upvotes: 2
tags: [agents, code-generation, evaluation, benchmarks, vibe-coding, software-engineering]
github: "https://github.com/snowmountainAi/webdevbench"
---

# SWE-WebDevBench: Evaluating Coding Agent Platforms as Virtual Software Agencies

> A 68-metric evaluation framework that assesses AI app-building ("vibe coding") platforms as **virtual software development agencies** — evaluating requirement understanding, architectural decisions, production code quality, iterative modifications, and business readiness across 6 platforms.

## Key Contributions

1. **Agency-angle evaluation**: First benchmark to evaluate AI coding platforms not as code generators but as complete software agencies — testing PM behavior, architecture decisions, and production readiness
2. **Three-dimensional evaluation cube**: Interaction Mode (ACR vs AMR) × Agency Angle (PM, Architect, Developer) × Complexity Tier — isolating specific axes of variation
3. **68 metrics across 7 groups**: 25 primary + 43 diagnostic metrics covering business intent, schema design, frontend engineering, security, performance, and canary requirement retention
4. **Four key findings**: Specification bottleneck (inadequate requirement elicitation), frontend-backend decoupling (UI quality ≠ backend quality), production readiness cliff (12–60 dev-hours post-generation), widespread security failures (no platform >65% security score)
5. **Canary requirements**: Novel technique embedding domain-specific requirements that only genuine comprehension (not template matching) would produce

## Method

### Evaluation Cube
- **Interaction Mode**: App Creation Request (ACR) vs App Modification Request (AMR) — building vs iterating
- **Agency Angle**: PM Agent (requirement elicitation), Architect (schema/infrastructure decisions), Developer (code quality)
- **Complexity Tier**: Medium (ExamEdge — EdTech) vs Complex (FieldForce — Field Service, MedSecure — Healthcare)

### 68 Metrics Taxonomy
| Group | Metrics | Examples |
|---|---|---|
| Business Intent (G1) | 3 | Feature completeness, canary retention, business inference |
| Schema & Data (G2) | 4 | Schema design, migration readiness, data integrity |
| Frontend (G3) | 4 | Component architecture, responsive design, accessibility |
| Backend (G4) | 4 | API design, error handling, async operations |
| Security (G5) | 4 | Auth implementation, data protection, input validation |
| Performance (G6) | 3 | Load handling, caching, query optimization |
| Modification (G7) | 3 | Change isolation, regression prevention, scope management |

### Judge Taxonomy
- **Tier 0**: Fully automated (HTTP tests, Lighthouse, k6 load tests, npm audit)
- **Tier 1**: LLM judges with structured prompts
- **Tier 2**: Human expert evaluation for nuanced judgments

## Results

### Cross-Platform Findings
- **No platform exceeds 60%** overall engineering score
- Every platform has at least one metric below 15%
- Production readiness is universally unsolved

### Four Critical Findings

1. **Specification Bottleneck**: Platforms compress rich business requirements into oversimplified technical plans. PM questioning ranges from 1 to 15 questions — more questions correlates with better canary retention (100% vs 21%)
2. **Frontend-Backend Decoupling**: Comparable frontend scores diverge dramatically on backend — polished UI masks infrastructure deficiency
3. **Production Readiness Cliff**: Every platform requires 12–60 developer-hours post-generation. The gap is 5× across platforms
4. **Security Failures**: No platform exceeds 65% security score (target: 90%). Common: hard-coded API keys, missing CSRF, absent rate limiting, JWT implementation errors

## Connections

- [[sources/swe-agent|SWE-agent]] — Evaluates coding agents on issue patches; SWE-WebDevBench evaluates full application platforms
- [[sources/qwen25-coder|Qwen2.5-Coder]] — SOTA code model; SWE-WebDevBench evaluates platforms built on such models
- [[concepts/agents|LLM Agents]] — Evaluates the full agentic stack from PM to deployment
- [[comparisons/code-models-agents|Code Models & Agents]] — Extends evaluation from code generation to software agency
- [[sources/kernelbenchx|KernelBench-X]] — Both benchmark code AI beyond function-level generation
