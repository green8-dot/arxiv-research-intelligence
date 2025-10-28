# Gap 3: Bridge Detection

Identifies papers bridging disconnected research communities.

## Methodology

**Community Detection:** Louvain algorithm on citation graph

**Bridge Criteria:**
- Cites ≥3 different communities
- Cited by ≥2 different communities
- High betweenness centrality

**Scoring:**
```
Score = 0.35 × cross_citations
      + 0.25 × semantic_similarity
      + 0.20 × betweenness
      + 0.15 × author_interdisciplinarity
      + 0.05 × citation_velocity
```

**Categories:** 0.80+ (strong), 0.60-0.79 (moderate), <0.60 (weak)

## Status

Implementation complete (1,100+ lines). Awaiting Neo4j Phase 2 (citation extraction).

## Citation

```bibtex
@misc{green2025bridges,
  title={Interdisciplinary Bridge Detection: Cross-Field Connections in Research},
  author={Green, Derek},
  year={2025}
}
```
