---
name: paper-analyze
description: Use when user runs /paper-analyze <arxiv_id> to deeply analyze a single paper. Downloads metadata, extracts figures, and generates a structured Obsidian note with Chinese abstract translation, method analysis, results, and pros/cons.
---

# paper-analyze

Deep analysis of a single paper by arXiv ID.

## Usage

```
/paper-analyze 2504.12345
```

## Execution Steps

1. **Fetch metadata** — query arXiv API or PubMed depending on input type:
   - arXiv ID: `python "E:/paper-reading/00_Config/scripts/fetch_papers.py" --single <arxiv_id>`
   - Paper title/PMID: search PubMed via eutils to get PMID, DOI, full abstract

2. **Extract images** — run extract_images.py with appropriate flag:
   - arXiv: `python "E:/paper-reading/00_Config/scripts/extract_images.py" --arxiv-id <arxiv_id> --output "E:/paper-reading/20_Papers/images/<arxiv_id>"`
   - PubMed: `python "E:/paper-reading/00_Config/scripts/extract_images.py" --pmid <pmid> --output "E:/paper-reading/20_Papers/images/PMID<pmid>"`

3. **Generate note** — create `E:\paper-reading\20_Papers\<id>-<slug-title>.md`
   - Always include a `### 论文图片` section in 方法概述 with all extracted figures
   - Use `![[images/<folder>/figN_pM.png]]` syntax for each figure
   - Add `*Figure N（第M页）— [图注待补充]*` caption under each image

4. **Link to daily note** — append reference to today's `10_Daily/YYYY-MM-DD-daily.md`

## Note Structure

```markdown
# [Paper Title]

> **arXiv**: [2504.XXXXX](https://arxiv.org/abs/2504.XXXXX)
> **Authors**: Author A, Author B, Author C
> **Published**: YYYY-MM-DD | **Citations**: N
> **Venue**: Journal/Conference Name
> **Tags**: #心肌损伤 #单细胞测序 #deep-learning

---

## 摘要翻译与要点

[Chinese translation of abstract]

**核心贡献**:
- Point 1
- Point 2

---

## 研究背景与动机

[Why this problem matters, what gap it fills]

---

## 方法概述

[Method description with key figures]

![[images/<arxiv_id>/fig1.png]]
*Figure 1: [Caption]*

---

## 实验结果

[Key results, metrics, comparisons]

![[images/<arxiv_id>/fig2.png]]

---

## 研究价值评估

**优势**:
- ...

**局限性**:
- ...

---

## 与相关论文对比

| 方面 | 本文 | [[Related Paper 1]] | [[Related Paper 2]] |
|------|------|---------------------|---------------------|
| 方法 | ... | ... | ... |

---

## 关联笔记

- [[30_Topics/心肌损伤]]
- [[10_Daily/YYYY-MM-DD-daily]]
```

## Fallback

If arXiv source tarball unavailable, use WebFetch on `https://arxiv.org/abs/<arxiv_id>`
to get abstract and metadata, then generate note without figures.
