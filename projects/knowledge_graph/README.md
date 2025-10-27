# Knowledge Graph Project

Neo4j graph database with 135K+ research papers.

## Overview

Graph database storing arXiv scientific papers with citation networks, author relationships, and category associations.

## Scale

- **135,911 papers** preprocessed and stored
- **130,945 papers** in active Neo4j database
- **Sub-second query times** for complex graph traversals
- **Multi-tier author recovery:** 99.7% success rate

## Schema

### Node Types
- Paper (title, abstract, arXiv ID, publication date)
- Author (name, h-index, affiliation)
- Category (domain, sub-category, hierarchy)
- Institution (university, research lab)

### Relationship Types
- AUTHORED (Author → Paper)
- CITES (Paper → Paper)
- BELONGS_TO (Paper → Category)
- AFFILIATED_WITH (Author → Institution)
- COLLABORATES_WITH (Author → Author)

## Features

### Citation Networks
- Forward citations (papers citing this work)
- Backward citations (papers this work cites)
- Citation velocity tracking (temporal trends)

### Author Collaboration
- Co-authorship networks
- Research community detection
- Cross-domain collaboration analysis

### Category Hierarchies
- Domain-level categories (e.g., cs, math, physics)
- Sub-categories (e.g., cs.LG, cs.CL, cs.AI)
- Multi-label papers (papers spanning categories)

## Query Examples

**Find highly-cited papers in machine learning:**
```cypher
MATCH (p:Paper)-[:BELONGS_TO]->(c:Category {name: 'cs.LG'})
WHERE p.citation_count > 100
RETURN p.title, p.citation_count
ORDER BY p.citation_count DESC
LIMIT 10
```

**Find cross-domain collaboration:**
```cypher
MATCH (a1:Author)-[:AUTHORED]->(p1:Paper)-[:BELONGS_TO]->(c1:Category),
      (a1)-[:AUTHORED]->(p2:Paper)-[:BELONGS_TO]->(c2:Category)
WHERE c1.domain <> c2.domain
RETURN a1.name, c1.domain, c2.domain
```

## Implementation

**Note:** Production infrastructure code maintained privately. For collaboration: Contact via GitHub

See main paper: [paper/paper.pdf](../../paper/paper.pdf)
