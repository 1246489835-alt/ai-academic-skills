---
name: paper-search
description: Use when user runs /paper-search <query> to search existing paper notes in the Obsidian vault. Searches by title, author, keywords, and tags with relevance ranking.
---

# paper-search

Search existing paper notes in `E:\paper-reading\20_Papers\`.

## Usage

```
/paper-search 心肌损伤 单细胞
/paper-search author:Zhang 2024
/paper-search tag:deep-learning
```

## Execution

Use Grep to search the vault:

```bash
# Search by keyword in content
grep -r "<query>" "E:/paper-reading/20_Papers/" --include="*.md" -l

# Search by tag
grep -r "#<tag>" "E:/paper-reading/20_Papers/" --include="*.md" -l
```

## Query Syntax

| Prefix | Example | Searches |
|--------|---------|----------|
| (none) | `心肌损伤` | title + abstract + full content |
| `author:` | `author:Zhang` | author field only |
| `tag:` | `tag:deep-learning` | tags only |
| `year:` | `year:2024` | published year |
| `venue:` | `venue:Nature` | journal/conference |

## Output Format

```
Found 3 results for "心肌损伤":

1. [[20_Papers/2504.12345-myocardial-repair]] (Score: 95)
   Authors: Zhang et al. | 2024-03 | Citations: 42
   Match: "...单细胞测序揭示心肌损伤后关键细胞亚群..."

2. [[20_Papers/2412.67890-scRNA-heart]] (Score: 78)
   ...
```

## Relevance Scoring

- Title match: 50 points
- Tag/keyword match: 30 points
- Abstract match: 20 points
- Recency bonus: up to 10 points
