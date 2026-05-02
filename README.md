# eletromidia-doc

> Claude Code skill for generating branded Eletromidia documents (DOCX + PDF)

## What it does

Generates professionally formatted Eletromidia documents from structured JSON content. Produces both DOCX (editable) and PDF (print-ready) with full brand compliance:

- Eletro Orange (#FF4F00) accents and section titles
- Montserrat font family with full Unicode support (including Portuguese diacritics)
- Header/footer logos
- Branded tables with alternating row colors
- Smart page breaking — sections flow continuously instead of each getting a full page

## Portuguese (pt-BR) Support

Full support for Portuguese diacritics (ç, ã, õ, é, ê, á, ó, ú, í, â, ô, à). Content JSON files must be UTF-8 encoded. Always use proper Portuguese accents in the content — do not strip them.

## Install

```bash
npx skills add iskisraell/eletromidia-doc -g
```

## Use in Claude Code

In any conversation:

> "Generate a new Eletromidia document with what we've talked here"

Claude will extract content from the conversation, build the JSON, and run the generator.

## Manual use

```bash
# Install dependencies
pip install -r scripts/requirements.txt

# Generate from JSON
python scripts/generate.py content.json

# PDF only
python scripts/generate.py content.json --pdf-only

# DOCX only
python scripts/generate.py content.json --docx-only
```

## Content format

See [`references/content-schema.md`](references/content-schema.md) for the full JSON schema.

## Brand specs

See [`references/brand-guidelines.md`](references/brand-guidelines.md) for colors, typography, and layout rules.

## License

MIT
