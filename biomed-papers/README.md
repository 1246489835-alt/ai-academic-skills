# Biomed Papers

Search and recommend top biomedical journal papers matching your research interests, with automatic bilingual note generation.

## What It Does

Searches PubMed for recent publications in top-tier biomedical journals (Nature, Cell, Science, Circulation, JACC, etc.) that match configurable research keywords, then generates bilingual (EN/CN) Obsidian notes.

## Usage

```bash
/biomed-papers                                    # default keywords
/biomed-papers --keyword "myocardial injury single cell"
/biomed-papers --journal "Circulation"
```

## Supported Journal Pool

| Tier | Journals |
|------|----------|
| CNS | Nature, Cell, Science, Nature Medicine, Nature Cardiovascular Research |
| Cardiology Top | Circulation, JACC, European Heart Journal, Cardiovascular Research |
| General Top | The Lancet, JAMA, NEJM |

## Default Keyword Pool

- myocardial injury / cardiac injury / heart failure
- high altitude / hypoxia
- single cell / scRNA-seq / snRNA-seq
- exercise / overload / mechanotransduction
- macrophage / immune / metabolism

## Workflow

1. **PubMed Search** — Query PubMed E-utilities API for recent relevant literature
2. **Journal Filter** — Keep only papers from the specified top-tier journal pool
3. **Metadata Extraction** — Title, year, journal, full abstract
4. **Bilingual Note** — Translate title and abstract to Chinese
5. **Save** — Output as dated Obsidian markdown note

## Output

Notes are saved to your configured paper-reading vault with the format:
```
YYYYMMDD-biomed-papers.md
```

## Customization

Edit the keyword pool and journal list to match your research direction. The skill auto-combines keywords for broader coverage.

## License

MIT
