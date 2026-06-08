---
name: start-my-day
description: Use when user runs /start-my-day to get daily paper recommendations. Fetches recent arXiv papers and high-citation Semantic Scholar papers, scores them, and generates a daily Obsidian note with top recommendations and auto-analysis of top 3 papers.
---

# start-my-day

Daily paper discovery and recommendation for biomedical research.

## Overview

Fetches papers from arXiv (last 30 days) and Semantic Scholar (last 1 year, high-citation),
scores them on 4 dimensions, and generates a daily Obsidian note.

## Execution Steps

1. **Read config** — load `E:\paper-reading\00_Config\research-config.yaml`
2. **Fetch papers** — run the fetch script:
   ```bash
   python "E:/paper-reading/00_Config/scripts/fetch_papers.py" --output-dir "E:/paper-reading/10_Daily"
   ```
3. **Generate bilingual daily note** — run the generate script (produces EN+CN titles and abstracts):
   ```bash
   python "E:/paper-reading/00_Config/scripts/generate_daily.py"
   ```
4. **Auto-analyze top 3** — for each of the top 3 papers, invoke `/paper-analyze <arxiv_id>`
5. **Link keywords** — wrap known topic keywords in `[[double brackets]]` to link existing notes

## Daily Note Format

```markdown
# Daily Papers — YYYY-MM-DD

## Overview
Brief summary of today's paper landscape in your research area.

## Top Recommendations

### 1. [Paper Title](arxiv_url) ⭐⭐⭐⭐⭐
- **arXiv ID**: 2504.XXXXX
- **Authors**: Author A, Author B
- **Score**: 92/100 (Relevance: 38, Recency: 28, Popularity: 18, Quality: 8)
- **Summary**: One-sentence summary in Chinese.
- **Keywords**: [[心肌损伤]], [[单细胞测序技术]]
→ [[20_Papers/2504.XXXXX-title]] (detailed note auto-generated)

### 2. ...
```

## Scoring Formula

| Dimension | Weight | Source |
|-----------|--------|--------|
| Relevance | 40% | keyword match in title + abstract |
| Recency | 30% | days since publication (arXiv) |
| Popularity | 20% | citation count (Semantic Scholar) |
| Quality | 10% | journal/venue tier |

## Notes

- If `fetch_papers.py` fails, fall back to WebSearch for arXiv papers manually
- Always link keywords that match filenames in `30_Topics/` using `[[keyword]]`
- Top 3 papers must have arXiv IDs for auto-analysis to work
