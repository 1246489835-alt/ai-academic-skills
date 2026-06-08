# Paper Analyze

Deep analysis of a single paper by arXiv ID or PubMed ID, with automatic figure extraction and structured Obsidian note generation.

## What It Does

Fetches paper metadata, extracts all figures, and generates a comprehensive bilingual analysis note with Chinese abstract translation, method breakdown, results summary, and critical evaluation.

## Usage

```
/paper-analyze 2504.12345
```

Supports:
- arXiv IDs (e.g., `2504.12345`)
- Paper titles
- PubMed IDs (PMID)

## Workflow

1. **Fetch metadata** — Query arXiv API or PubMed E-utilities
2. **Extract images** — Run `extract_images.py` (source tarball → PDF fallback)
3. **Generate note** — Create structured Obsidian markdown with embedded figures
4. **Link** — Append reference to today's daily note

## Output Note Structure

```markdown
# [Paper Title]

> **arXiv**: [2504.XXXXX](https://arxiv.org/abs/2504.XXXXX)
> **Authors**: Author A, Author B, Author C
> **Published**: YYYY-MM-DD | **Citations**: N
> **Tags**: #心肌损伤 #单细胞测序 #deep-learning

---

## 摘要翻译与要点
[Chinese translation + core contributions]

## 研究背景与动机
[Problem context, gap identification]

## 方法概述
[Method description with extracted figures]
![[images/<arxiv_id>/fig1.png]]

## 实验结果
[Key results, metrics, comparisons]

## 研究价值评估
**优势**: ...
**局限性**: ...

## 与相关论文对比
[Comparison table with related work]

## 关联笔记
- [[30_Topics/心肌损伤]]
- [[10_Daily/YYYY-MM-DD-daily]]
```

## Key Features

- Bilingual output (Chinese analysis + English metadata)
- Automatic figure extraction and embedding
- Critical evaluation (strengths + limitations)
- Cross-referencing with related papers and topic notes
- Integration with daily paper discovery workflow

## Dependencies

- Python 3.8+
- `pdfplumber` (for PDF figure extraction)
- Internet access to arXiv / PubMed APIs

## License

MIT
