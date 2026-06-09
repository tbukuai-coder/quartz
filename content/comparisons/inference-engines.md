---
type: comparison
tags: [inference, serving, deployment, efficiency, synthesis]
---

# Comparison: Inference Engines (vLLM vs SGLang vs TGI)

> Side-by-side analysis of major open-source LLM serving frameworks.

## Feature Comparison

| Feature | [[sources/vllm\|vLLM]] | [[sources/sglang\|SGLang]] | TGI (HuggingFace) |
|---|---|---|---|
| **Core innovation** | PagedAttention | RadixAttention + Compressed FSM | Flash decoding, watermarking |
| **GitHub stars** | 77K+ | 20K+ | 12K+ |
| **Structured output** | Via Outlines/xgrammar | Native compressed FSM | Via Outlines |
| **Throughput gain** | 2–4× | Up to 6.4× | ~2× |
| **Quantization** | GPTQ, AWQ, FP8 | GPTQ, AWQ, FP8 | GPTQ, AWQ, EETQ |
| **OpenAI API** | ✅ | ✅ | ✅ |

## When to Choose

### vLLM — General-Purpose
Best for standard chat/completion, high-throughput batch, mixed workloads. Largest ecosystem, broadest hardware and quantization support.

### SGLang — Structured + Agentic
Best for JSON output, shared-prefix workloads, agent tool calls. RadixAttention reuses prefixes; compressed FSM is fastest structured output.

### TGI — HF Ecosystem
Best for HF Inference Endpoints, production deployments needing watermarking, teams already in HF ecosystem.

## Performance (Relative)

| Workload | vLLM | SGLang | TGI |
|---|---|---|---|
| Standard chat | ★★★★ | ★★★★ | ★★★ |
| Shared prefix | ★★★ | ★★★★★ | ★★★ |
| JSON / structured | ★★★ | ★★★★★ | ★★★ |
| Batch inference | ★★★★★ | ★★★★ | ★★★ |

## Trend
All three converging on feature parity. vLLM has largest community; SGLang gaining for agentic workloads; TGI default for HF-hosted.

## Key Papers
- [[sources/vllm]] — PagedAttention (2023)
- [[sources/sglang]] — RadixAttention + Compressed FSM (2023)

## See Also
- [[concepts/llm-serving]] — Serving concepts
- [[concepts/kv-cache]] — KV cache management
- [[concepts/structured-generation]] — Structured output
- [[concepts/post-training-quantization]] — Quantized serving