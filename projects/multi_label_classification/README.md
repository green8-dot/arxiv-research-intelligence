# Multi-Label Classification Project

Part of arXiv Research Intelligence Framework

## Results

- **94.26% F1** on computer science domain
- 8 categories simultaneously classified (cs.AI, cs.LG, cs.CL, cs.CV, cs.CR, cs.NE, cs.DC, cs.SE)
- 40,000 papers dataset
- SciBERT fine-tuned architecture

## Approach

High-level methodology:
1. SciBERT transfer learning (pre-trained on 1.14M papers)
2. Domain-specific fine-tuning on CS papers
3. Multi-label output layer (sigmoid activation per category)
4. Contamination cleaning (removed 20% mislabeled papers)

See [paper/paper.pdf](../../paper/paper.pdf)
