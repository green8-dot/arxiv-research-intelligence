# arXiv Research Intelligence Framework

**Research Paper:** Multi-Domain Label Noise Detection and Cleaning for Scientific Document Classification
**Status:** Submitted to arXiv (cs.LG, cs.CL) - Awaiting moderation approval
**Results:** 91.34% average F1 across 9 scientific domains

## Overview

Multi-domain scientific document classification system achieving 91.34% F1 score across 9 arXiv domains (122,911 papers). Combines SciBERT transfer learning with contamination cleaning methodology for systematic label noise detection and removal.

**Key Achievements:**
- 91.34% average F1 across math, physics, stats, economics, biology, and more
- 94.26% F1 on computer science (8 categories, 40K papers)
- 20-60% label contamination detected and cleaned per domain
- 135K+ papers in Neo4j knowledge graph
- 96% precision on mislabel detection

## Research Paper

**Title:** Multi-Domain Label Noise Detection and Cleaning for Scientific Document Classification
**Author:** Derek Green
**Submitted:** October 26, 2025
**Category:** cs.LG (Machine Learning), cs.CL (Computation and Language)
**PDF:** [paper/paper.pdf](paper/paper.pdf)
**LaTeX Source:** [paper/paper.tex](paper/paper.tex)

**Abstract:**

Label noise in scientific document classification datasets presents a significant challenge to achieving high accuracy, particularly when categories are semantically overlapping or exhibit severe class imbalance. This work presents a contamination cleaning methodology that identifies and removes mislabeled samples from arXiv scientific paper datasets across 10 diverse domains. Using SciBERT as a baseline classifier, the approach trains on raw data, extracts prediction disagreements as contamination candidates, removes them, and retrains on cleaned data. This methodology achieves 91.35% average validation accuracy across 10 arXiv domains (46 categories total), with all domains exceeding 85% accuracy. Contamination rates range from 20-60% per domain, with cleaning improving accuracy by 8-15 percentage points in most cases.

## Results

### Domain Performance

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
| **Average** | **22** | **122,911** | **91.34%** |

**Computer Science Domain** (separate evaluation):
- 8 categories (cs.AI, cs.LG, cs.CL, cs.CV, cs.CR, cs.NE, cs.DC, cs.SE)
- 40,000 papers
- **94.26% F1 score**

See [results/RESULTS_SUMMARY.md](results/RESULTS_SUMMARY.md) for detailed metrics.

## Methodology

### High-Level Approach

1. **Transfer Learning:** SciBERT fine-tuned on domain-specific corpora
2. **Contamination Detection:** Train baseline → identify prediction disagreements → extract mislabeled candidates
3. **Label Cleaning:** Remove contamination (20-60% per domain)
4. **Retraining:** Train on cleaned data → 85-95% accuracy achieved
5. **Validation:** Cross-domain validation and confidence analysis

### Key Findings

- Label noise significantly degrades performance (10-15% loss)
- Contamination cleaning improves F1 by 8-15 percentage points
- SciBERT transfer learning provides strong baseline across scientific domains
- Single methodology generalizes to diverse scientific fields

See [methodology/](methodology/) for conceptual descriptions.

## Projects

This repository integrates four research projects:

### 1. Multi-Label Classification ([projects/multi_label_classification/](projects/multi_label_classification/))

SciBERT-based classification achieving 94% F1 on computer science papers.

**Key Features:**
- 8-category multi-label classification
- Transfer learning from 1.14M pre-trained papers
- Data quality validation

### 2. Category Validator ([projects/category_validator/](projects/category_validator/))

Systematic mislabel detection in arXiv papers.

**Results:**
- 182 mislabels found in cs.DC (3.5% error rate)
- 96% precision
- Cross-validation methodology

### 3. Knowledge Graph ([projects/knowledge_graph/](projects/knowledge_graph/))

Neo4j graph database with 135K+ research papers.

**Features:**
- Sub-second query times
- Citation networks
- Author collaboration graphs
- 6 node types, 8 relationship types

### 4. Research Synthesis ([projects/research_synthesis/](projects/research_synthesis/))

Automated research intelligence gathering and NLP processing.

## Implementation Details

**Note:** This repository contains research findings and methodology. Production implementation code (training pipelines, infrastructure configs, proprietary optimizations) is maintained privately.

**For collaboration or implementation details:** derekg124@yahoo.com

## Documentation

- [methodology/OVERVIEW.md](methodology/OVERVIEW.md) - High-level approach
- [methodology/CONTAMINATION_DETECTION.md](methodology/CONTAMINATION_DETECTION.md) - Label cleaning concepts
- [results/RESULTS_SUMMARY.md](results/RESULTS_SUMMARY.md) - Detailed performance metrics
- [docs/CITATION.md](docs/CITATION.md) - How to cite this work

## Citation

**BibTeX:**
```bibtex
@article{green2025arxiv,
  title={Multi-Domain Label Noise Detection and Cleaning for Scientific Document Classification},
  author={Green, Derek},
  journal={arXiv preprint},
  year={2025},
  note={Submitted to cs.LG, cs.CL}
}
```

*(arXiv ID will be added upon publication approval)*

## License

MIT License - See [LICENSE](LICENSE) for details.

Research findings freely available for academic and commercial use.

## Acknowledgments

- SciBERT model: AllenAI
- arXiv dataset: Cornell University
- Neo4j graph database

## Contact

**Derek Green**
Email: derekg124@yahoo.com
LinkedIn: [linkedin.com/in/derekgreen-44723323a](https://linkedin.com/in/derekgreen-44723323a)
GitHub: [@green8-dot](https://github.com/green8-dot)

---

**Status:** Research complete, paper submitted to arXiv (awaiting approval), implementation details available on request.
