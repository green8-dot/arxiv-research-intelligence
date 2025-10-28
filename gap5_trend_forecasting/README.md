# Gap 5: Trend Forecasting

Predicts emerging research areas 6-12 months before peak.

## Methodology

**Citation Velocity:** `velocity = total_citations / years_since_publication` (threshold: >5× domain average)

**Cross-Domain Emergence:** Topics gaining traction across multiple domains simultaneously

**Author Migration:** Senior researchers (h-index >30) switching to new topics

**Temporal Clustering:** SciBERT clustering over time (2020-2025), track exponential growth

**Scoring:**
```
Confidence = 0.40 × citation_velocity
           + 0.30 × cluster_growth
           + 0.20 × author_migration
           + 0.10 × cross_domain
```

**Categories:** 0.80+ (high), 0.60-0.79 (moderate), <0.60 (weak)

## Status

Implementation complete. Awaiting Neo4j citation data for testing.

## Citation

```bibtex
@misc{green2025trends,
  title={Research Trend Forecasting: Predicting Emerging Scientific Areas Using Citation Velocity},
  author={Green, Derek},
  year={2025}
}
```
