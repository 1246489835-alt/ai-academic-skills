# Nature Polishing

Polish, restructure, or translate academic prose into Nature-leaning English for high-impact journal submission.

## What It Does

A multi-level academic writing refinement skill that works at both structural (section logic, argument flow) and sentence level (clarity, concision, hedging). Built from writing-strategy course notes and Academic Phrasebank patterns.

## Usage

```
/nature-polishing
```

Apply to: abstracts, introductions, results, discussions, conclusions, titles, methods sections, or Chinese academic drafts.

## Core Philosophy

> Language serves argument. Do not polish sentences while leaving the reasoning broken.

The skill diagnoses before editing:

```
paper type → section job → paragraph logic → claim/evidence/boundary → sentence polish
```

## Key Features

### Structural Level
- Paper type identification (research, methods, hypothesis-based, algorithmic)
- Hourglass structure enforcement (broad → narrow → broad)
- Section responsibility checks (Results ≠ Discussion)
- Reader-first ordering: relevance → novelty → trust → reuse → meaning

### Sentence Level
- 10-30 word target range, hard cap at 30
- One proposition per sentence
- No em dashes in polished output
- Results vs Discussion syntax separation

### Chinese-to-English Mode
- Extracts core propositions first (no clause-by-clause translation)
- Reconstructs explicit logical links
- Verifies terminology, causality, hedging, disciplinary nuance

## Section Guidance

| Section | Core Job |
|---------|----------|
| Introduction | Why it matters + what gap + how addressed |
| Results | What happened (past tense, quantitative) |
| Discussion | How we understand it + when it may fail |
| Conclusion | Three-part close: contribution → evidence → bounded implication |
| Title | Curiosity with credibility |
| Abstract | Mini-paper: context → gap → approach → results → implication |
| Methods | Specific, complete, transparent, reproducible |

## AI Traffic-Light Boundary

| Level | Acceptable Use |
|-------|----------------|
| 🟢 Green | Grammar, clarity, outline, alternative phrasings, translation |
| 🟡 Yellow | Method explanation, reviewer-response frameworks (with human check) |
| 🔴 Red | Drafting core argument, inserting unchecked references/data |

## Output Format

1. Polished text (plain prose)
2. Revision notes (3-5 bullets on major changes)
3. Section logic changes flagged explicitly

## Reference Files

- `references/published-article-patterns.md` — Nature/Nat Commun article patterns
- `references/writing-strategy.md` — Paragraph and section argument repair
- `references/section-moves.md` — Section-specific move orders
- `references/phrasebank-playbook.md` — Hedging, transition, evidence phrases
- `references/style-guardrails.md` — Academic style checks and mechanics

## License

MIT
