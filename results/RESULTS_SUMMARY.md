# Results Summary

## Overall Performance

**Average F1 Score:** 91.34% across 9 arXiv domains

## Domain-Specific Results

| Domain | Categories | Papers | F1 Score |
|--------|-----------|--------|----------|
| Math | 4 | 24,715 | 93.97% |
| Stats | 2 | 8,447 | 92.26% |
| Nucl | 1 | 3,891 | 92.72% |
| Hep | 1 | 15,239 | 92.64% |
| Eess | 1 | 4,892 | 92.57% |
| Econ | 1 | 2,847 | 92.43% |
| Physics | 10 | 47,283 | 88.88% |
| Nlin | 1 | 4,127 | 88.51% |
| Qbio | 1 | 11,470 | 88.04% |
| **Total** | **22** | **122,911** | **91.34%** |

## Computer Science Domain (Separate Evaluation)

- 8 categories (cs.AI, cs.LG, cs.CL, cs.CV, cs.CR, cs.NE, cs.DC, cs.SE)
- 40,000 papers
- **94.26% F1 score**

## Contamination Detection

**Label Noise Rates (per domain):**
- 20-60% contamination detected in raw datasets
- Systematic label correction improves F1 by 8-15 percentage points
- Category validation identifies mislabeled papers with 96% precision

## Key Findings

1. **SciBERT Effectiveness:** Transfer learning from 1.14M scientific papers provides strong baseline
2. **Contamination Impact:** Label noise significantly degrades performance (10-15% loss)
3. **Cleaning Methodology:** Model-corrected label detection achieves consistent 85-95% accuracy after cleaning
4. **Domain Generalization:** Single methodology works across diverse scientific domains

## Detailed Results

Individual domain results available in:
- `math_simple_results.json`
- `stats_simple_results.json`
- `physics_simple_results.json`
- `qbio_simple_results.json`
- `nlin_simple_results.json`
- `econ_simple_results.json`
- `eess_simple_results.json`
- `hep_simple_results.json`
- `nucl_simple_results.json`

Each file contains:
- Test F1 score
- Test accuracy
- Training history
- Category-specific metrics
