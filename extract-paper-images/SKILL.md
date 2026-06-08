---
name: extract-paper-images
description: Use when extracting figures from a paper by arXiv ID. Tries arXiv source tarball first for high-quality images, falls back to PDF extraction with pdfplumber. Saves to vault images directory.
---

# extract-paper-images

Extract figures from arXiv papers into the Obsidian vault.

## Usage

```
/extract-paper-images 2504.12345
```

Or called automatically by `paper-analyze`.

## Execution

```bash
python "E:/paper-reading/00_Config/scripts/extract_images.py" \
  --arxiv-id <arxiv_id> \
  --output "E:/paper-reading/20_Papers/images/<arxiv_id>"
```

## Strategy

**Priority 1 — arXiv source tarball** (highest quality):
1. Download `https://arxiv.org/src/<arxiv_id>`
2. Extract `.tar.gz` → find `.pdf`, `.png`, `.eps`, `.jpg` files
3. Convert `.eps` to `.png` if needed

**Priority 2 — PDF extraction** (fallback):
1. Download `https://arxiv.org/pdf/<arxiv_id>`
2. Use `pdfplumber` to extract embedded images
3. Filter out small images (< 100x100px) and logos

## Output

```
E:\paper-reading\20_Papers\images\<arxiv_id>\
├── fig1.png
├── fig2.png
├── fig3.png
└── index.md     ← image index with captions
```

`index.md` format:
```markdown
# Figures: <arxiv_id>

- ![[fig1.png]] — Figure 1: [caption if extractable]
- ![[fig2.png]] — Figure 2: ...
```

## Notes

- If both methods fail, report which figures are missing and provide arXiv figure URL pattern
- Always save index.md even if only some figures extracted
