# Nature Data

Prepare, audit, and revise Nature-ready Data Availability statements, repository plans, dataset citations, and FAIR metadata checklists.

## What It Does

Guides you through creating publication-ready Data Availability sections for Nature-family journal submissions. Covers repository selection, accession numbers, dataset citations, restricted data handling, and FAIR compliance.

## Usage

```
/nature-data
```

Trigger phrases:
- "数据可用性声明"
- "Data Availability statement"
- "数据存储库选择"
- "FAIR metadata"
- "受限数据处理"

## Workflow

1. **Identify** target journal and article type
2. **Inventory** all datasets supporting main and supplementary results
3. **Classify** each dataset's access route (public repo, controlled access, within paper, third-party restricted, etc.)
4. **Choose** repository and identifier strategy (DOI, accession number, Handle, ARK)
5. **Draft** Data Availability statement with dataset-to-location mapping
6. **Add** formal dataset citations for public data
7. **Audit** FAIR and metadata compliance
8. **Return** ready-to-paste statement + unresolved fields

## Output Format

```text
Data Availability
[ready-to-paste statement in English]

Repository and citation actions
- [specific actions needed]

Missing information / risk flags
- [items author must confirm]

中文核对
- [用中文列出需确认的字段]
```

## Key Features

- Bilingual support (Chinese input → English submission-ready output)
- Conservative stance: never invents DOIs, accession numbers, or licenses
- Flags "available upon request" as weak unless legally justified
- Separates data, code, materials, and protocols
- Supports all access routes: public, controlled, restricted, reused, supplementary

## Access Route Classification

| Route | When to Use |
|-------|-------------|
| Public repository | Standard open data (GEO, Zenodo, Dryad, etc.) |
| Controlled access | Human genomic data (dbGaP, EGA) |
| Within paper | Source data figures, supplementary tables |
| Third-party restricted | Licensed databases, clinical records |
| On justified request | Legal/ethical restrictions with review process |

## Reference Files

- `references/policy-principles.md` — Nature/Springer Nature data-sharing rules
- `references/chinese-author-alignment.md` — CN-to-EN terminology alignment
- `references/statement-patterns.md` — Ready-to-adapt statement templates
- `references/repository-and-identifiers.md` — Repository choice and DOI guidance
- `references/fair-metadata-checklist.md` — FAIR checks and DataCite fields

## License

MIT
