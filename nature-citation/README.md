# Nature Citation

Turn manuscript text into defensible CNS-level citations with reference-manager export.

## What It Does

Segments your manuscript text into citable units, searches Crossref and PubMed for matching Nature/Science/Cell family papers, evaluates support strength, and exports a ready-to-import reference file (.enw/.ris/.rdf).

## Usage

```
/nature-citation
```

Trigger phrases:
- "给这段文字补引用"
- "Nature系列引用"
- "CNS及子刊支撑文献"
- "分段引用"
- "导出EndNote/RIS/Zotero"

## Workflow

1. **Segment** — Split text into citable units (S001, S002, ...)
2. **Parse** — Extract core claim, identify claim type and entities
3. **Search** — Query Crossref + PubMed with multiple search strategies
4. **Evaluate** — Grade each candidate: `strong` / `partial` / `background` / `contradictory` / `metadata-only`
5. **Export** — Generate reference-manager file + interactive HTML browser
6. **Report** — Structured output with support grades and risk flags

## Scope Options

| Scope | Coverage |
|-------|----------|
| `cns` | Cell, Nature, Science + major sister journals |
| `nature` | Nature Portfolio only |
| `flagship` | Nature, Science, Cell only |

## Output

```
交互式引用浏览器
- citation_visualization.html

分段引用对应关系
S001: [segment text]
  - Author, Year, Title, Journal, DOI
  - 支撑等级: strong/partial/background
  - 插入建议: after sentence 2

导出文件
- references.enw

风险和缺口
- [missing areas or contradictory evidence]
```

## Long Article Strategy

| Segments | Strategy |
|----------|----------|
| 1–10 | Single run, full inline analysis |
| 11–25 | Batch mode (`--batch-size 10`), compact summary |
| 26+ | Split by section, process independently, merge |

## Key Features

- Bilingual support (Chinese input, English search, Chinese notes)
- Conservative support grading (never cites metadata-only candidates as evidence)
- HTML interactive browser for filtering and selecting candidates
- Multiple export formats: ENW, RIS, Zotero RDF
- Publication time filtering with `--from-year` / `--to-year`

## License

MIT
