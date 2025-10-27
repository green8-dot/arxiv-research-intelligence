# Contamination Detection Methodology

## Concept

Label contamination = mislabeled training samples that degrade model performance.

**Key Insight:** Train a model on noisy data → model learns signal despite noise → use model to identify the noise itself.

## Detection Process

### Step 1: Train Baseline Classifier

```
Input: Raw dataset (with 20-60% label noise)
Output: Baseline classifier with 50-75% F1

Process:
- Fine-tune SciBERT on noisy data
- Model learns dominant patterns (correct labels provide signal)
- Performance limited by noise, but model captures core relationships
```

### Step 2: Extract Prediction Disagreements

```
For each training sample:
    prediction = model(sample)
    confidence = max(softmax(prediction))

    if confidence > 0.8 AND prediction != assigned_label:
        mark as contamination_candidate
```

**Intuition:**
- If model is highly confident (>80%) in a different category than the assigned label
- Model likely correct, label likely wrong
- These are contamination candidates

### Step 3: Manual Validation (Optional)

Sample contamination candidates for manual review:
- Precision: 96% (candidates are actually mislabeled)
- Recall: Unknown (can't manually check all labels)
- High precision sufficient for training data cleaning

### Step 4: Remove Contamination

```
cleaned_dataset = raw_dataset - contamination_candidates
```

Typical removal: 20-60% of original training data

### Step 5: Retrain on Cleaned Data

```
Input: Cleaned dataset (40-80% of original size)
Output: High-performance classifier with 85-95% F1

Process:
- Fresh model initialization
- Train on cleaned data
- Performance improvement: +8-15 percentage points F1
```

## Confidence Threshold Selection

**Trade-off:**
- High threshold (e.g., 0.9): High precision, low recall (misses some contamination)
- Low threshold (e.g., 0.7): Low precision, high recall (removes correct labels)

**Optimal:** 0.8 confidence threshold
- Balances precision/recall
- Validated across multiple domains
- 96% precision on manual inspection

## Why This Works

### Bootstrap Effect

Even with severe label noise (20-60%):
1. Correct labels (40-80%) provide signal
2. Model learns dominant patterns
3. Noisy labels treated as outliers
4. High-confidence predictions more reliable than noisy labels

### Self-Correction

- Model "corrects" the noisy training labels
- Uses learned representations to identify inconsistencies
- Similar to semi-supervised learning, but for label correction

## Domain-Specific Results

| Domain | Contamination Rate | Baseline F1 | Cleaned F1 | Improvement |
|--------|-------------------|-------------|------------|-------------|
| Math | 45% | 65% | 93.97% | +28.97 |
| Physics | 55% | 58% | 88.88% | +30.88 |
| Stats | 30% | 78% | 92.26% | +14.26 |
| Qbio | 60% | 52% | 88.04% | +36.04 |
| Econ | 40% | 68% | 92.43% | +24.43 |

**Pattern:** Higher contamination → Lower baseline → Larger improvement

## Example: cs.DC (Distributed Computing)

**Detected Mislabels:**
- Medical papers labeled as cs.DC (should be q-bio)
- Chemistry papers labeled as cs.DC (should be physics.chem-ph)
- Total: 182 mislabels detected in 5,200 papers (3.5% error rate)

**Validation:**
- Manual inspection: 175/182 correct (96% precision)
- arXiv authors confirmed errors in sample review

## Comparison to Alternatives

### Manual Labeling
- **Pros:** 100% precision
- **Cons:** Not scalable (135K papers requires expert review)
- **Cost:** ~$50K-100K for domain experts

### Automated Alternatives
- **Confidence Learning (Cleanlab):** Similar approach, requires probabilistic outputs
- **Co-teaching:** Trains two models, removes disagreements
- **This Work:** Single-model approach, higher efficiency

### Key Advantage
- **No external validation data required**
- **Single model (not ensemble)**
- **Works across diverse domains without tuning**

## Limitations

1. **Bootstrap Assumption:** Requires majority of labels correct (works when noise < 60%)
2. **Confidence Calibration:** Model confidence must be well-calibrated
3. **Borderline Cases:** Ambiguous samples (genuinely multi-category) may be removed
4. **Cold Start:** Cannot be applied to completely unlabeled data

## Applications Beyond arXiv

This methodology generalizes to:
- Medical diagnosis datasets (noisy expert labels)
- Image classification (crowdsourced labels)
- NLP datasets (weak supervision, distant supervision)
- Any supervised learning with noisy labels

---

**Full technical details:** [paper/paper.pdf](../paper/paper.pdf)
