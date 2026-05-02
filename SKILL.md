---
name: eletromidia-doc
description: >
  Generate branded Eletromidia documents (DOCX + PDF) from conversation context.
  Use this skill when the user asks to "generate an eletromidia document", "create a branded doc",
  "write a formal document for eletromidia", or references the Eletromidia document template.
  Produces properly formatted documents with Eletromidia branding (orange #FF4F00, Montserrat font,
  header/footer logos, professional tables). Full Portuguese (pt-BR) diacritics support.
---

Generate branded Eletromidia documents in both DOCX and PDF formats from conversation context.

## When to Use

- User asks to generate a formal Eletromidia document, report, plan, or proposal
- User references "eletromidia document", "eletromidia template", or "branded doc"
- User says "generate a new eletromidia document with what we've talked here"

## Process

1. Extract content from conversation context: titles, sections, subsections, bullet points, tables
2. Determine document metadata: authors, date, classification, version
3. Build a JSON content file following the schema in `references/content-schema.md`
4. Run `scripts/generate.py <content.json>` to produce DOCX and PDF
5. Report output file paths to user

## Content Schema

Structure the content as JSON. See `references/content-schema.md` for the full schema.

Key fields:
- `title`: main title (uppercase, bold)
- `subtitle`: array of subtitle lines
- `meta`: array of `{label, value}` pairs for the cover page
- `sections`: array of section objects with `title`, optional `body`, `bullets`, `tables`, `subsections`

## Portuguese (pt-BR) Support

The generator fully supports Portuguese diacritics. When writing content in pt-BR:

- **Always use proper accents**: ç, ã, õ, é, ê, á, ó, ú, í, â, ô, à
- **Do not strip accents** from Portuguese words (e.g., write "seção", not "secao"; "métricas", not "metricas")
- The JSON file must be saved as UTF-8 (which is the default for the Write tool)
- Montserrat TTF fonts embed all Latin Extended glyphs needed for Portuguese

## Page Layout Behavior

- **Cover page** always gets its own page (page break after cover)
- **Sections flow continuously** — no forced page break between sections
- Smart page break: a new page is added only when <45mm of space remains before a section title
- This produces compact documents instead of wasting pages on small sections

## Brand Guidelines

See `references/brand-guidelines.md` for colors, fonts, and layout rules.

Quick reference:
- Primary orange: `#FF4F00`
- Font: Montserrat (Regular, Bold, Italic, BoldItalic)
- Header logo: top-left, 48x14mm
- Footer logo: centered, 5.2x9.4mm
- Page counter: bottom-right, number only

## Output

- DOCX: Microsoft Word compatible, editable
- PDF: Print-ready, with Montserrat fonts embedded
- Both saved to the user's Downloads folder (or specified path)

## Dependencies

- Python 3.8+ with `fpdf2` and `python-docx` packages
- Fonts and logos bundled in `assets/`
- No external network required (fully offline)

## References

- `references/content-schema.md` — JSON input schema
- `references/brand-guidelines.md` — Eletromidia brand specs
- `scripts/generate.py` — Document generator script
- `scripts/requirements.txt` — Python dependencies
