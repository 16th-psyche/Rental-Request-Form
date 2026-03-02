# Equipment Rental Request Builder

A single-page web app for creating, previewing, and exporting professional equipment rental request documents as PDF. Built for **Quantum Leap Learning Solutions** using plain HTML, CSS, and JavaScript — no framework, no build step, no installation.

## Live Demo

[https://16th-psyche.github.io/Rental-Request-Form/](https://16th-psyche.github.io/Rental-Request-Form/)

Or open `index.html` directly in any modern browser.

## Features

- **Live preview** — the rendered document updates in real time as you type
- **Dynamic equipment table** — add or remove rows for each piece of rented equipment
- **Zoom controls** — scale the preview from 40% to 120%
- **PDF export** — downloads a print-ready A4 PDF named after your project
- **Form validation** — highlights missing required fields before export
- **No dependencies** — one external CDN script (`html2pdf.js`) is the only dependency

## Getting Started

No installation or build step required.

```bash
# Clone the repo
git clone <repo-url>

# Open directly in a browser
open "Rent requirement/index.html"
```

Or simply double-click `index.html` in Finder / File Explorer.

## Usage

1. **Fill in the form** on the left panel:
   - Document submission date (auto-filled to today)
   - Project name, requester name, contact, email, and vendor
   - Delivery and return dates, times, and locations
   - Equipment list — item name, quantity, and remarks per row
   - Notes / special instructions

2. **Preview** your document live on the right panel. Use **−** / **+** to zoom in or out.

3. Click **Download PDF** to export. The file is named `rental-request-<project-name>.pdf`.

## Project Structure

```
Rent requirement/
└── index.html   # Entire app — HTML, CSS (~400 lines), and JS (~215 lines) in one file
```

All logic, styles, and markup are self-contained in `index.html`.

### Key JavaScript Globals

| Variable | Type | Description |
|---|---|---|
| `rows` | `Array<{item, qty, remarks}>` | Equipment table state |
| `zoomLevel` | `number` | Current preview scale (default `1.0`) |

### Core Functions

| Function | Description |
|---|---|
| `updatePreview()` | Reads form values and updates the live preview DOM |
| `renderRows()` | Rebuilds the equipment input rows from `rows` array |
| `addRow()` / `removeRow(i)` | Mutates `rows` and re-renders |
| `setZoom(delta)` / `applyZoom()` | Adjusts and applies preview scale |
| `downloadPDF()` | Validates, then exports the preview as a PDF via html2pdf.js |
| `esc(str)` | Escapes HTML entities to prevent XSS |
| `fmtDate(val)` / `fmtTime(val)` | Formats date/time picker values for display |

## Tech Stack

| Technology | Role |
|---|---|
| HTML5 | Document structure |
| CSS3 (Flexbox / Grid) | Layout and design system |
| Vanilla JavaScript (ES6+) | All app logic and state |
| [html2pdf.js v0.10.1](https://github.com/eKoopmans/html2pdf.js) (CDN) | PDF generation |
| Apple system font stack | Typography (no external fonts) |

## Design System

CSS custom properties drive the visual language:

| Token | Value | Usage |
|---|---|---|
| `--accent` | `#ffc938` | Golden yellow — buttons, badges, focus rings |
| `--accent-hover` | `#e6b200` | Hover state |
| `--surface` | `#FFFFFF` | Card/form background |
| `--surface-2` | `#F2F2F7` | Page background |
| `--danger` | `#FF3B30` | Errors, remove button |
| `--radius` | `14px` | Card corners |

Layout: fixed 400px left sidebar (form) + flexible right panel (preview). The preview renders at A4 dimensions (794×1122 px) and scales via CSS `transform: scale()`.

## Browser Support

Any modern browser that supports:
- CSS `backdrop-filter`
- `FileReader` API
- ES6+ (`const`, arrow functions, template literals, `Array.map`)

Tested in Chrome and Safari.

## License

MIT
