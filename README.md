# EXAMFLOW V0.8 — chunked browser AI prototype

This GitHub Pages frontend-only build fixes the small-model context overflow by splitting extracted PDF text into short segments and processing them sequentially.

## Deploy
Upload the contents of this folder to the root of your GitHub repository, replacing the previous files. Keep `.github/workflows/page.yml` or `pages.yml` (either filename works) and select GitHub Actions in Settings → Pages.

## Changes from V0.7
- AI processes short text segments instead of sending the entire 10-page document in one prompt.
- Progress indicates segment number.
- Merges and de-duplicates candidate MCQs.
- Only complete four-option questions are offered for approval.
- Missing answer keys remain unverified; teacher must select a correct answer before quiz creation.
- Footer and PDF review note updated to V0.8.

## Use
1. Preview PDF.
2. For scanned PDFs, select OCR language and run OCR.
3. Load browser AI model (WebGPU required).
4. Click AI structure OCR text. Wait while segments are processed.
5. Inspect/edit every candidate, verify the answer against the original PDF, tick approval, then add to bank.

## Limitations
- This is still experimental browser AI. The 0.5B model may miss questions, misread scientific notation, or return malformed JSON.
- Chunking reduces context-window overflow; it does not guarantee extraction accuracy.
- PDF OCR accuracy depends on image quality, columns, Gujarati/Hindi glyphs, formulas and diagrams.
- Answer keys are not reliably inferable from question text. Do not publish without checking the source.
- No backend, persistent database, secure accounts, or private exam links. Browser URL sharing exposes answer data; demo use only.
- First use downloads OCR language data and the WebLLM model. No customer-side installation or API key is required.
