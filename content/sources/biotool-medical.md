---
type: source
arxiv_id: "2605.05758"
title: "BioTool: A Comprehensive Tool-Calling Dataset for Enhancing Biomedical Capabilities of Large Language Models"
authors: ["Xin Gao", "Ruiyi Zhang", "Meixi Du", "Peijia Qin", "Pengtao Xie"]
date: 2026-05
tags: [tool-use, biomedical, fine-tuning, llm, ncbi, genomics, proteomics, dataset]
upvotes: 0
---

# BioTool: A Comprehensive Tool-Calling Dataset for Enhancing Biomedical Capabilities of Large Language Models

> A comprehensive biomedical tool-calling dataset covering NCBI, Ensembl, UniProt, and other domain-specific APIs, enabling LLMs to effectively leverage biomedical tools for clinical research and genomics.

## Key Contributions
- Identifies that LLMs perform poorly on biomedical tasks because they cannot effectively leverage the tools clinical experts and researchers use daily
- Creates a comprehensive biomedical tool-calling dataset covering key databases and APIs:
  - **NCBI**: National Center for Biotechnology Information (PubMed, Gene, Nucleotide, etc.)
  - **Ensembl**: Genome browser and gene annotation
  - **UniProt**: Protein sequence and functional information
  - Other genomics, proteomics, and evolution research tools
- Demonstrates that fine-tuning on BioTool enables LLMs to outperform commercial alternatives on biomedical tasks
- Provides API call pairs for training tool-calling capabilities in the biomedical domain

## Method
The dataset construction:
1. Curated domain-specific APIs relevant to biomedical research (genomics, proteomics, evolution)
2. Generated high-quality query-API-call pairs covering realistic use cases
3. Ensured coverage of complex multi-step tool interactions typical in biological workflows
4. Evaluated fine-tuned models against commercial biomedical LLM tools

## Results
- LLM fine-tuned on BioTool dataset demonstrates superior biomedical task performance compared to commercial alternatives
- Effective tool-calling in genomics, proteomics, and evolutionary biology contexts

## Datasets Used
- NCBI databases (PubMed, Gene, Nucleotide)
- Ensembl genome browser
- UniProt protein database

## Models Released
- GitHub: https://github.com/gxx27/BioTool (0 stars)

## Connections
- Related: [[sources/toolformer]] — general tool-calling framework
- Related: [[sources/codeact]] — code as actions for agents
- Related: [[sources/eywa]] — heterogeneous agentic framework
- Related concept: [[concepts/agents]], [[concepts/structured-generation]]

## Citation
> Gao et al., "BioTool: A Comprehensive Tool-Calling Dataset for Enhancing Biomedical Capabilities of Large Language Models," arXiv:2605.05758, 2026.
