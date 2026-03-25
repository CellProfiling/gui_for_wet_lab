# 384 Well Plate Metadata GUI

A browser-based GUI for designing **384-well plate layouts** and exporting structured, per-well metadata — primarily built for single-cell proteomics workflows using LC-MS/MS.

> **No installation required.** Download `plate_layout_gui.html` and open it in any web browser.

---

## ▶️ Quick Start

1. Download **`plate_layout_gui.html`** (click the file above → click the download button ⬇)
2. Double-click the file to open it in Chrome, Firefox, Safari, or Edge
3. Fill in your experiment info, design your plate layout, and click **Export**

> ⚠️ Requires an internet connection on first use — the app loads React and SheetJS from a CDN.  
> Once your browser has cached those, it works offline too.

---

## ✨ What It Does

You fill in experiment details and draw your plate layout using an interactive 16 × 24 grid.  
Labels are painted onto wells by clicking and dragging. The tool then exports:

- ✅ A **per-well metadata Excel file** (`.xlsx`) — one row per well, all layout layers merged
- ✅ A **reloadable session file** (`.json`) — reload your layout later to continue editing

---

## 🖥️ Interface Overview

### Home screen
- **Experiment date** — enter in `YYYYMMDD` format (e.g. `20260327`)
- **Experiment name** — short identifier (e.g. `TWC02`)
- **Extra metadata** — add any additional key–value fields you want in the output (e.g. `LC_method: 25min_gradient`, `MS_method: DIA`)
- **Entries** — the list of plate layout layers you've defined (e.g. master mix, cell sorting, LC-MS acquisition)

### Grid editor (per entry)
- **Labels** — define your own label names (e.g. `A`, `B`, `0cell`, `1MG`, `TRUE`)
- **Paint mode** — click a label to activate it, then click-and-drag on the grid to paint wells
- **Rectangle / Freehand / Eraser** — switch between drawing modes
- **Fill Empty / Fill All** — quickly flood wells with the active label
- **Well count** — live count of how many wells carry each label
- **Split into multiple columns** — if a label encodes more than one thing (e.g. `1cellA` = 1 cell, type A), map it to separate output columns

---

## 📤 Output Files

### Excel file — `YYYYMMDD_expName_metadata.xlsx`

| Sheet | Contents |
|-------|----------|
| `metadata` | **Main output.** One row per well, all fields merged. |
| `summary` | Well counts grouped by condition combination. |
| *(one sheet per entry)* | Raw 16 × 24 grid view of each layout layer. |
| `_session` | Session JSON embedded for reference. |

**Example `metadata` columns:**

| experiment | date | LC_method | MS_method | Well | Row | Column | master_mix | number_of_cells | cell_type | to_LCMS_acquisition |
|---|---|---|---|---|---|---|---|---|---|---|
| TWC02 | 20260327 | 25min_gradient | DIA | A1 | A | 1 | A | 0 | — | True |
| TWC02 | 20260327 | 25min_gradient | DIA | E1 | E | 1 | A | 1 | MG | True |

### Session file — `YYYYMMDD_expName_session.json`

Saves everything you entered. Use **Load Session** in the app to restore a previous layout exactly as you left it.

---

## 🗂️ Example Files

The `examples/` folder contains a working example you can try:

| File | Description |
|------|-------------|
| `20260101_example_session.json` | Load this in the app to see the example layout |
| `20260101_example_metadata.xlsx` | The Excel output generated from that session |

**To load the example:** open `plate_layout_gui.html` → click **Load Session** → select `20260101_example_session.json`

---

## 🛠️ Technical Notes

The tool is a self-contained HTML file. It uses:

| Library | Purpose | How it's loaded |
|---------|---------|-----------------|
| [React 18](https://react.dev) | UI framework | CDN |
| [Babel Standalone](https://babeljs.io) | JSX compilation in browser | CDN |
| [SheetJS (xlsx)](https://sheetjs.com) | Excel file export | CDN |

No server, no Python, no `npm install` — everything runs in the browser.

---

## 📸 Screenshots

Please see screenshots folder for some example of using this GUI tool

---

## 🐛 Known Limitations

- Plate size is fixed at 384 wells (16 rows × 24 columns)
- Requires internet connection on first open (CDN libraries)
- Date should be entered in `YYYYMMDD` format
