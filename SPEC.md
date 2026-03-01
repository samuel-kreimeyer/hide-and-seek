# PDF Label Locator - Specification (MVP)

## Goal
Create a single-page, self-contained web app that runs from a local HTML file with no install step and no internet requirement.

## Primary User Story
As an estimator, I can:
1. Open the local web page.
2. Upload a PDF construction drawing.
3. Enter a search string and page range.
4. Run a search.
5. View all matched instances in a table with page number and `(X, Y)` in inches.
6. Download results as CSV with default filename based on the entered search string (fallback: `users-search-string.csv`).

## Functional Requirements
1. The app is one HTML file containing all CSS and JavaScript needed to run.
2. User inputs:
   - PDF file selector.
   - Search string text field.
   - Page range field supporting forms like `1-3, 5, 9-10`.
3. Search behavior:
   - Search text extracted from PDF pages within selected range.
   - Match all occurrences in each text item (case-insensitive for MVP).
4. Output table columns:
   - Row number.
   - Page number.
   - X (in).
   - Y (in).
   - Matched text snippet.
5. Coordinates:
   - Use PDF coordinate space.
   - Positive X is to the right.
   - Positive Y is up.
   - Convert points to inches (`in = points / 72`).
6. CSV export:
   - Export currently displayed table rows.
   - Default name: sanitized search string + `.csv`; if empty after sanitize, use `users-search-string.csv`.

## Validation and Errors
1. Require PDF file before search.
2. Require non-empty search string.
3. Validate page range:
   - Numeric entries and ranges only.
   - Clamp to PDF page count.
   - Error when nothing valid remains.
4. Show clear status messages for loading, searching, errors, and result count.

## Non-Goals (MVP)
1. OCR for scanned/non-selectable text PDFs.
2. Geometry-accurate per-glyph positions in complex transformed text.
3. Fuzzy matching and regex search.
4. Persistent local storage.

## Technical Notes
1. Embed PDF parsing library code in the HTML to preserve offline behavior.
2. Use no build tooling or package manager at runtime.
3. Keep implementation browser-native and dependency-free for end users.

## Acceptance Criteria (MVP)
1. Opening `index.html` locally shows a usable UI without network access.
2. A text-based PDF can be searched by term and page range.
3. Results show page and coordinates in inches.
4. CSV download works and opens in spreadsheet tools.
