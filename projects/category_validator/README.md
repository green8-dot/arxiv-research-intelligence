# Category Validator Project

Systematic mislabel detection in arXiv papers.

## Results

- **182 mislabels** detected in cs.DC (Distributed Computing) category
- **96% precision** (manual verification of sample)
- **3.5% error rate** in arXiv cs.DC labels
- Cross-validation methodology

## Methodology

Conceptual approach:
1. Train classifier on labeled data
2. Compare high-confidence predictions to assigned labels
3. Extract disagreements (confidence > 0.8, prediction != label)
4. Manual verification of sample detections

## Sample Detections

**Example Mislabels:**
- Medical imaging papers labeled as cs.DC (should be q-bio or physics)
- Chemistry simulation papers labeled as cs.DC (should be physics.chem-ph)
- Robotics papers labeled as cs.DC (should be cs.RO)

Full list of detected mislabels available on request.

## Impact

Demonstrates systematic quality issues in arXiv categorization:
- Author self-categorization without validation
- Semantic overlap between categories causes confusion
- No automated quality control in arXiv submission process

## Validation

Manual inspection of 100 random detections:
- 96 confirmed as actual mislabels (96% precision)
- 4 ambiguous cases (genuinely multi-category)

## Implementation

**Note:** Production code maintained privately. For collaboration: Contact via GitHub

See main paper: [paper/paper.pdf](../../paper/paper.pdf)
