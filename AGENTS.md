# AGENTS.md

## Quick start
- **No build step.** Open `index.html` in a browser directly or serve with `python3 -m http.server 8080`.
- All code lives in `index.html` (single self-contained file).

## Project architecture
- Two-phase UX: **Input view** (paste poem + load `.txt` file) → **Memorize view** (revealed poem).
- Data flow: `parsePoem(text)` → `stanzas[stanzaIdx][lineIdx][wordIdx]` where each word is `{original, leading, core, trailing, individualReveal}`.
- Two stacked reveal modes: **global reveal level** (← → arrow keys) and **per-word reveal** (click a word, capped at the word's own length).
- `getDisplayText(word)` returns `Math.max(globalRevealLevel, word.individualReveal)` characters of `core` — no underscores or placeholders for hidden letters.
- `.gitignore` ignores `*.txt`; existing `.txt` data files are force-tracked.

## Gotchas
- No tests, linter, formatter, or type checker.
- Two near-duplicate function pairs exist: `updateSpan`/`updateSpanElement` and `updateAllSpans`/`refreshAllSpans`. The latter in each pair includes null checks and is the more robust variant.
- All changes go in `index.html`. There is no other source file to edit.

## Style conventions
- **No React** — always plain HTML, vanilla JS, minimal dependencies.
- **CSS:** 2-space indent, start with `* { box-sizing: border-box; }`.
- **Inputs/textareas:** `font-size: 16px`; font prefers Helvetica.
- **JS:** 2-space indent, `<script type="module">`, top-level code not indented.
- **Headings:** Sentence case.
