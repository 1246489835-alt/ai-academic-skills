# Start My Day

Daily paper discovery and recommendation system with automatic scoring and analysis.

## What It Does

Fetches papers from arXiv (last 30 days) and Semantic Scholar (last 1 year, high-citation), scores them on 4 dimensions, generates a daily Obsidian note with top recommendations, and auto-analyzes the top 3 papers in depth.

## Usage

```
/start-my-day
```

Run each morning to discover the most relevant new papers in your research area.

## Workflow

1. **Load config** — Read research interests from `research-config.yaml`
2. **Fetch papers** — Run `fetch_papers.py` (arXiv + Semantic Scholar)
3. **Score & rank** — Apply 4-dimension scoring formula
4. **Generate daily note** — Bilingual (EN + CN) Obsidian note
5. **Auto-analyze top 3** — Deep analysis via `paper-analyze` for highest-scored papers
6. **Link keywords** — Wrap known topics in `[[double brackets]]`

## Scoring Formula

| Dimension | Weight | Source |
|-----------|--------|--------|
| Relevance | 40% | Keyword match in title + abstract |
| Recency | 30% | Days since publication |
| Popularity | 20% | Citation count (Semantic Scholar) |
| Quality | 10% | Journal/venue tier |

## Daily Note Format

```markdown
# Daily Papers — YYYY-MM-DD

## Overview
Brief summary of today's paper landscape.

## Top Recommendations

### 1. [Paper Title](arxiv_url) ⭐⭐⭐⭐⭐
- **arXiv ID**: 2504.XXXXX
- **Authors**: Author A, Author B
- **Score**: 92/100 (Relevance: 38, Recency: 28, Popularity: 18, Quality: 8)
- **Summary**: One-sentence summary in Chinese
- **Keywords**: [[心肌损伤]], [[单细胞测序技术]]
→ [[20_Papers/2504.XXXXX-title]] (detailed note)

### 2. ...
```

## Configuration

Edit `research-config.yaml` to customize:
- Research keywords and topics
- Journal tier definitions
- Scoring weights
- Output directory

## Dependencies

- Python 3.8+
- `arxiv` API access
- Semantic Scholar API access
- Obsidian vault structure

## License

MIT
