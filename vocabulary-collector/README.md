# Vocabulary Collector

Extract words, phrases, and sentences from web content and create bilingual vocabulary notes in Obsidian.

## What It Does

Turns highlighted or pasted English content into structured bilingual (EN/CN) vocabulary notes, organized by date with full contextual translations.

## Usage

```
/vocabulary-collector
```

Then paste any English content — articles, paragraphs, word lists, or highlighted sentences.

## Workflow

1. **Receive content** — User pastes words, phrases, sentences, or article excerpts
2. **Extract** — Identify key expressions, idioms, metaphors, counter-intuitive ideas, and core arguments
3. **Translate** — Full bilingual output with context
4. **Save** — Append to today's note or create new themed note

## Output Format

```markdown
## 1. English word/phrase/sentence

**释义**：中文释义（词性/用法说明）
> Original English sentence with context
对应的中文翻译（完整句子双语对照）
```

## File Structure

```
vocabulary-collector/
├── 20260403/
│   ├── 20260403-productivity-books-reading.md
│   └── 20260403-business-strategy-growth.md
├── 20260404/
│   └── 20260404-health-fitness-nutrition.md
```

## Naming Rules

- Date folders: `YYYYMMDD/`
- Note files: `YYYYMMDD-keyword1-keyword2-keyword3.md`
- Same-day content appends to existing note by default
- New note created only when user specifies new keywords

## Extraction Priority

1. Metaphors and figurative language
2. Counter-intuitive viewpoints
3. Author's core arguments
4. Useful idioms and collocations
5. Domain-specific terminology

## Key Features

- Full bilingual translations (not word-for-word, but natural Chinese)
- Preserves original context and tone
- Date-based organization for spaced review
- Obsidian-compatible markdown
- Automatic append for same-day content

## License

MIT
