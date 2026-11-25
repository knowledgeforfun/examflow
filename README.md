# EXAMFLOW V0.7 — Browser OCR + AI PDF-to-Quiz prototype

This is a **GitHub Pages frontend-only prototype**. It requires no customer-side software installation and no API key.

## Publish
1. Create a GitHub repository.
2. Upload the contents of this folder to the repository root.
3. Open Settings → Pages.
4. Select **GitHub Actions** as the deployment source.
5. The included `.github/workflows/pages.yml` deploys the static site on pushes to `main`.
6. Open the published URL after the Actions workflow succeeds.

## New features
- PDF.js renders uploaded PDF pages in the browser.
- PDF.js extracts selectable text when the PDF contains a usable text layer.
- Tesseract.js performs browser-side OCR for English, English+Hindi, or English+Gujarati. Language data downloads on first use.
- A conservative pattern parser proposes MCQs from extracted/OCR text.
- Optional WebLLM browser model (`Qwen2.5-0.5B-Instruct-q4f16_1-MLC`) can be loaded where WebGPU and sufficient memory are available.
- AI can structure the extracted text into candidate MCQs. It is instructed not to invent missing content, but outputs can still be wrong.
- Teacher review controls allow editing, selecting a detected answer key, and explicitly approving each question before adding it to the question bank.
- Quiz creation and student preview remain available.

## Browser and device requirements
- Modern desktop browser recommended (Chrome or Edge recent version).
- Internet connection required for PDF.js, Tesseract.js, language data, and WebLLM model download.
- OCR may be slow on long PDFs. Browser memory and CPU/GPU capacity matter.
- WebLLM requires WebGPU support; some devices/browsers will not support it. The OCR + manual-review workflow remains available without AI.
- Browser model downloads can be hundreds of MB or more, depending on model/runtime. Model loading may fail on low-memory devices.

## Language and document limitations
- Hindi/Gujarati OCR quality depends on scan resolution, font, skew, columns, equations and language model quality.
- Multi-column layouts, tables, diagrams, mathematical notation, answer keys printed separately, and mixed scripts may be misread.
- This build runs OCR page-by-page on rendered PDF pages. It does not promise reliable extraction from every arbitrary PDF.
- The parser only proposes questions when it recognizes common numbering and A–D option patterns. Unusual formats need manual correction.
- Answer keys and solutions are not reliably inferred from question text. If no answer key is found, teacher must select/verify the answer. Never treat a model-generated answer as verified.
- AI extraction is a convenience, not a source of truth. Check every question, option, answer and solution against the original PDF before publishing.

## Privacy and security
- PDF processing occurs locally in the browser tab; this package does not upload the PDF to a server.
- OCR language data and the AI runtime/model are downloaded from public CDNs/model hosting. Do not use confidential papers unless the user has approved those external downloads.
- Quiz share links in this prototype encode quiz data in the URL fragment. This is **not secure**: answer keys may be visible to anyone who inspects the link. Use only non-confidential demos.
- Questions, uploaded files and results are not synchronized across users/devices. No real authentication, institute separation, database or secure exam session exists.

## Demo steps
1. Open PDF Review.
2. Select a PDF and click Preview PDF pages.
3. Choose OCR language and click Run OCR for scanned PDFs.
4. Optionally click Load browser AI model (WebGPU required), then AI structure OCR text.
5. Edit each candidate and mark the teacher approval checkbox.
6. Select the correct answer only after checking the original source.
7. Click Add approved questions to bank.
8. Create a quiz and open its demo link in another tab.

## Future production architecture
For public/institute accounts, private PDFs, secure share links, server-side answer checking, large-scale OCR and shared analytics, add a hosted API, database, private object storage and background workers. GitHub Pages remains a suitable static frontend host, not a backend.
