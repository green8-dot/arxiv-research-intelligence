# arXiv Research Intelligence

Multi-domain classification, knowledge graphs, research gap analysis.

**Paper:** Multi-Domain Label Noise Detection and Cleaning for Scientific Document Classification
**Status:** Submitted to arXiv (cs.LG, cs.CL) - October 26, 2025
**Results:** 91.34% F1 across 9 domains

## Components

**Core:** Multi-domain classification with label noise detection
- 91.34% F1 (9 domains, 122,911 papers)
- 94.26% F1 (CS: 8 categories, 40K papers)
- 20-60% contamination cleaned per domain
- 165K papers in Neo4j graph

**Gap Extensions:**
- Gap 2: Reproducibility scoring (0-100 scale)
- Gap 3: Bridge detection (cross-community)
- Gap 5: Trend forecasting (citation velocity)

## Paper

[paper/paper.pdf](paper/paper.pdf) | [paper/paper.tex](paper/paper.tex)

**Abstract:** Contamination cleaning methodology for arXiv paper classification. SciBERT baseline trained on noisy data identifies mislabeled samples via prediction disagreements. Removes contamination, retrains on cleaned data. 91.35% average accuracy across 10 domains (46 categories), all >85%. Contamination: 20-60% per domain. Cleaning improves accuracy by 8-15 points.

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

**CS Domain:** 94.26% F1 (8 categories, 40K papers)

[results/RESULTS_SUMMARY.md](results/RESULTS_SUMMARY.md)

## Methodology

1. SciBERT fine-tuned on domain-specific corpora
2. Train baseline → identify prediction disagreements → extract mislabeled candidates
3. Remove contamination (20-60% per domain)
4. Retrain on cleaned data → 85-95% accuracy
5. Cross-domain validation

[methodology/](methodology/)

## Projects

1. **Multi-Label Classification** - 94% F1, 8 categories, 40K papers ([projects/multi_label_classification/](projects/multi_label_classification/))
2. **Category Validator** - 182 mislabels found in cs.DC, 96% precision ([projects/category_validator/](projects/category_validator/))
3. **Knowledge Graph** - Neo4j, 135K papers, citation networks ([projects/knowledge_graph/](projects/knowledge_graph/))
4. **Research Synthesis** - Automated intelligence gathering ([projects/research_synthesis/](projects/research_synthesis/))

## Gap Extensions

### Gap 2: Reproducibility Scoring

0-100 scale: code availability, data availability, methodology completeness, citation network.
Status: Implementation complete. [gap2_reproducibility/](gap2_reproducibility/)

### Gap 3: Bridge Detection

Louvain community detection, cross-community citations, author migration, multi-signal scoring.
Status: Implementation complete, awaiting citation data. [gap3_bridge_detection/](gap3_bridge_detection/)

### Gap 5: Trend Forecasting

Citation velocity, cross-domain emergence, author migration, temporal clustering.
Status: Implementation complete, awaiting citation data. [gap5_trend_forecasting/](gap5_trend_forecasting/)

## Documentation

- [methodology/OVERVIEW.md](methodology/OVERVIEW.md)
- [methodology/CONTAMINATION_DETECTION.md](methodology/CONTAMINATION_DETECTION.md)
- [results/RESULTS_SUMMARY.md](results/RESULTS_SUMMARY.md)
- [docs/CITATION.md](docs/CITATION.md)

## Citation

```bibtex
@article{green2025arxiv,
  title={Multi-Domain Label Noise Detection and Cleaning for Scientific Document Classification},
  author={Green, Derek},
  journal={arXiv preprint},
  year={2025},
  note={Submitted to cs.LG, cs.CL}
}
```

## License

MIT License - [LICENSE](LICENSE)


