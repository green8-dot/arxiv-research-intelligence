# Methodology Overview

## Problem Statement

Scientific document classification faces two primary challenges:
1. **Label Noise:** 20-60% of arXiv papers are mislabeled due to author self-categorization errors
2. **Domain Diversity:** Scientific domains have varying characteristics (terminology, structure, category overlap)

Traditional approaches either accept noisy labels (degrading performance) or require manual validation (not scalable).

## Approach

### 1. Baseline Training

Train SciBERT classifier on raw (noisy) data:
- Fine-tune `allenai/scibert_scivocab_uncased` on domain-specific papers
- Multi-label classification head
- Typical performance: 50-75% F1 (limited by label noise)

### 2. Contamination Detection

Identify mislabeled samples by comparing model predictions to assigned labels:
- Extract high-confidence predictions that disagree with labels
- Threshold: Prediction confidence > 0.8, disagreement with assigned label
- These are "contamination candidates"

### 3. Label Cleaning

Remove contamination candidates from training data:
- Contamination rates: 20-60% per domain (systematic pattern)
- Remaining data: High-quality labeled samples
- Validation: Manual inspection shows 96% precision on detected mislabels

### 4. Retraining

Train on cleaned data:
- Same architecture, fresh initialization
- Cleaned training set (40-80% of original size)
- Performance improvement: +8-15 percentage points F1
- Final performance: 85-95% F1 across all domains

## Key Insights

**Why This Works:**

1. **Bootstrap from Noisy Data:** Even with 20-60% noise, SciBERT learns enough signal to identify mislabels
2. **High-Confidence Disagreements:** Model predictions that strongly disagree with labels are usually correct
3. **Domain Generalization:** Same methodology works across math, physics, biology, economics, etc.

**Contamination Sources:**

- Author self-categorization errors (e.g., physics paper labeled as computer science)
- Semantic overlap between categories (e.g., computational biology vs. bioinformatics)
- arXiv allows authors to select categories without validation

## Architecture

### Model

- **Base:** SciBERT (`allenai/scibert_scivocab_uncased`)
- **Pre-training:** 1.14M scientific papers
- **Fine-tuning:** Domain-specific datasets (2K-50K papers per domain)
- **Classification Head:** Single linear layer (SciBERT embeddings → category logits)

### Training

- **Optimizer:** AdamW
- **Learning Rate:** 2e-5 (standard for SciBERT fine-tuning)
- **Epochs:** 6-10 for baseline, 10-15 for cleaned data
- **Batch Size:** 16-32 (GPU memory dependent)
- **Sequence Length:** 128 tokens (title + abstract)

### Evaluation

- **Metrics:** F1 score (primary), Accuracy
- **Validation:** 20% holdout set
- **Test:** Independent test set (10-20% of data)
- **Cross-validation:** Results validated across multiple domains

## Results Summary

**Performance:**
- 91.34% average F1 across 9 domains
- 94.26% F1 on computer science (8 categories)
- All domains exceed 85% F1 after cleaning

**Contamination Detection:**
- 20-60% label noise per domain
- 96% precision on mislabel detection (manual verification)
- Consistent pattern across diverse scientific fields

**Generalization:**
- Single methodology, no domain-specific tuning
- Works for high-dimensional (46 categories) and low-dimensional (2 categories) problems
- Robust to class imbalance

## Limitations

1. **Bootstrap Requirement:** Needs sufficient signal in noisy data (works when noise < 60%)
2. **Confidence Threshold:** Requires tuning for optimal precision/recall trade-off
3. **Computational Cost:** Two full training cycles (baseline + retrain)
4. **Manual Validation:** Precision estimates require manual inspection of sample

## Applications

- Automated literature review (accurate categorization)
- Research gap identification (find misclassified papers)
- Data quality assessment (measure label noise in datasets)
- Scientific knowledge graphs (populate with high-quality labels)

---

**Full details:** See paper [paper/paper.pdf](../paper/paper.pdf)
