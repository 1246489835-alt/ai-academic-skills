# Extract Paper Images

Extract figures from arXiv papers into your Obsidian vault with automatic indexing.

## What It Does

Downloads and extracts high-quality figures from scientific papers using a two-tier strategy: arXiv source tarball first (highest quality), PDF extraction as fallback.

## Usage

```
/extract-paper-images 2504.12345
```

Also called automatically by the `paper-analyze` skill.

## Extraction Strategy

| Priority | Method | Quality |
|----------|--------|---------|
| 1 | arXiv source tarball (.tar.gz) | Highest — original vector/raster files |
| 2 | PDF extraction via pdfplumber | Good — embedded raster images |

### Priority 1 — Source Tarball
1. Download `https://arxiv.org/src/<arxiv_id>`
2. Extract archive, find `.pdf`, `.png`, `.eps`, `.jpg` files
3. Convert `.eps` to `.png` if needed

### Priority 2 — PDF Fallback
1. Download `https://arxiv.org/pdf/<arxiv_id>`
2. Extract embedded images with `pdfplumber`
3. Filter out small images (< 100x100px) and logos

## Output Structure

```
images/<arxiv_id>/
├── fig1.png
├── fig2.png
├── fig3.png
└── index.md     ← image index with captions
```

### index.md Format

```markdown
# Figures: <arxiv_id>

- ![[fig1.png]] — Figure 1: [caption if extractable]
- ![[fig2.png]] — Figure 2: ...
```

## Dependencies

- Python 3.8+
- `pdfplumber`
- Internet access to arXiv

## License

MIT
