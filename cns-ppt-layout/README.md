# CNS PPT Layout

Auto-arrange scientific figures into Nature/Cell/Science submission-grade PPT layouts.

## What It Does

Takes named research figures (tif/png/jpg) and automatically assembles them into portrait A4 PPTX slides with Nature-standard panel labels, intelligent height allocation, aspect-ratio preservation, and tight rectangular packing.

**Does NOT generate figures** (use `/nature-figure` for that). This skill only handles **layout assembly** of existing images.

## Usage

```
/cns-ppt-layout "C:\path\to\figures"
```

Trigger phrases: "排版", "PPT排版", "Figure排版", "CNS排版", "Nature排版"

## Naming Convention

Images must follow the `【letter-number】` pattern:

```
【a-1】celltype_umap.tif        → Panel a, image 1
【a-2】cell_proportion.tif      → Panel a, image 2
【b】qc_violin.tif              → Panel b, single image
【c-1】GO_heatmap_up.tif        → Panel c, image 1
【c-2】GO_heatmap_down.tif      → Panel c, image 2
```

## Folder Structure

### Single folder (main or supplementary only)
```
figures/
  【a-1】xxx.tif
  【b】xxx.tif
```
→ Generates 1 slide

### Main + Supplementary
```
figures/
  【1】主图/
    【a】xxx.tif
    【b】xxx.tif
  【2】附图/
    【a-1】xxx.tif
    【b-1】xxx.tif
```
→ Generates 2 slides (Slide 1 = Main, Slide 2 = Supplementary)

## Layout Specifications

| Parameter | Value |
|-----------|-------|
| Page size | 7.5 × 10.0 inches (portrait, A4-like) |
| Background | White (#FFFFFF) |
| Panel labels | Bold lowercase (a, b, c...), Arial 12pt |
| Margins | Left/Right 0.7cm, Top 0.7cm, Bottom 0.4cm |
| Panel gap | Vertical: 0.45cm |
| Image gap | Horizontal within panel: 0.2cm |

## Core Layout Principles

1. **Rectangular packing** — Final layout must form a tight rectangle with minimal whitespace
2. **Tile thinking** — Panels are puzzle pieces that snap together, not centered in isolated zones
3. **Area balance** — Multi-image panels shouldn't be visually much smaller than single-image panels
4. **Width saturation** — Side-by-side panels must fill ≥97% of available page width
5. **AR-based height** — Row heights calculated from actual aspect ratios, not arbitrary percentages
6. **No unnecessary pagination** — Scale down before splitting across pages
7. **Label visibility** — Panel labels never obscured by images

## Layout Logic

| Image Count | Default Layout |
|-------------|---------------|
| 1 (wide, AR>2) | Full width, own row |
| 1 (square, AR≈1) | Must pair with adjacent panel |
| 1 (tall, AR<0.8) | Must pair with adjacent panel |
| 2 | Side by side |
| 3 | Three equal columns |
| 4 | Four columns or 2×2 grid |
| 5+ | 3+2 or 2+3 adaptive |

## Parameter Overrides

- `横版` → Switch to 16:9 landscape (13.33 × 7.5 in)
- `大标签` → Label size = 14pt
- `紧凑` → Reduced gaps
- `宽松` → Increased gaps

## Output

- PPTX file with Nature-standard layout
- Companion Python script for parameter tweaking
- Layout summary (panel count, image count, aspect ratios)
- Slide notes with panel descriptions (auto-extracted from filenames)

## Relationship with Other Skills

```
/nature-figure   → Generate individual publication-quality plots
/cns-ppt-layout  → Assemble finished plots into Figure-level PPT
```

Typical workflow: `/nature-figure` first → `/cns-ppt-layout` second.

## Dependencies

- Python 3.x
- python-pptx
- Pillow (PIL)

## License

MIT
