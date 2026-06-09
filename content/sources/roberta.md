---
type: source
arxiv_id: "1907.11692"
title: "RoBERTa: A Robustly Optimized BERT Pretraining Approach"
authors: ["Yinhan Liu", "Myle Ott", "Naman Goyal", "et al."]
date: 2019-07-26
org: "Meta AI"
tags: [foundational, encoder, pre-training, nlp]
upvotes: 2
---

# RoBERTa: Robustly Optimized BERT

> Showed that **BERT was significantly undertrained** — by training longer, on more data, with larger batches, and removing next-sentence prediction, RoBERTa matched or exceeded all post-BERT models. Established that **training recipe optimization** can be as impactful as architectural innovation. Still widely used as a base model for fine-tuning.

## Key Contributions
- **BERT was undertrained**: Simply training longer with better hyperparameters closes the gap with GPT-2 and XLNet
- **Removed NSP**: Next Sentence Prediction objective hurts performance — removed it
- **More data, longer training**: 160GB of text (vs. BERT's 16GB), trained for 500K steps
- **Dynamic masking**: Generate new masks each epoch (vs. BERT's static masks)
- **Larger batches**: 8K batch size improves perplexity

## Key Findings
| Change | Effect |
|---|---|
| Remove NSP | Improved downstream performance |
| Dynamic masking | Marginal improvement |
| More data (160GB vs 16GB) | Significant improvement |
| Longer training (500K vs 100K steps) | Significant improvement |
| Larger batch (8K vs 256) | Improved perplexity |

## Results
| Model | MNLI | QNLI | SST-2 | SQuAD |
|---|---|---|---|---|
| BERT-Large | 86.6 | 92.3 | 93.2 | 90.9 |
| **RoBERTa-Large** | **90.2** | **94.7** | **96.4** | **94.6** |
| XLNet-Large | 89.8 | 93.9 | 95.6 | 94.5 |

RoBERTa matches or exceeds XLNet (which introduced complex permutation-based training) with simple recipe improvements.

## Impact
- **Still widely used**: RoBERTa-base/large remain popular for classification fine-tuning
- **Recipe > architecture**: Established that training recipe matters more than model architecture
- **GaLore experiments**: [[sources/galore|GaLore]] validates on RoBERTa fine-tuning
- **Base for DeBERTa**: [[sources/deberta|DeBERTa]] builds on RoBERTa's training approach
- **Sentence-transformers**: Many SBERT models use RoBERTa as backbone
- Influenced the "train longer, train better" philosophy adopted by LLaMA, Chinchilla

## Connections
- Builds on: [[sources/bert|BERT]]
- Extended by: [[sources/deberta|DeBERTa]], [[sources/distilbert|DistilBERT]] (distilled variants)
- Org: [[entities/orgs/meta|Meta AI]]
- Concepts: [[concepts/pre-training]], [[concepts/fine-tuning]]

## Citation
> Liu et al., "RoBERTa: A Robustly Optimized BERT Pretraining Approach," arXiv:1907.11692, 2019.
