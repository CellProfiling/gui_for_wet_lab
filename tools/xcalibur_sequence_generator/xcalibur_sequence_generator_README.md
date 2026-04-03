# Xcalibur Sequence Generator

A browser-based GUI for generating **Xcalibur LC-MS sequence files** from 384-well plate metadata — built for single-cell proteomics workflows on Thermo Orbitrap instruments.

> **No installation required.** Download `xcalibur_sequence_generator.html` and open it in any web browser.

---

## ▶️ Quick Start

1. Download **`xcalibur_sequence_generator.html`** (click the file above → click the download button ⬇)
2. Double-click the file to open it in Chrome, Firefox, Safari, or Edge
3. Upload your metadata `.xlsx` (from `plate_layout_gui.html`), fill in run settings, select wells, and click **▶ Generate**

> ⚠️ Requires an internet connection on first use — the app loads SheetJS from a CDN.  
> Once your browser has cached it, it works offline too.

---

## ✨ What It Does

Takes a per-well metadata Excel file (from the **384 Well Plate Metadata GUI**) and generates a ready-to-import Xcalibur sequence with:

- QC bracketing: Blank → BSA QC → HeLa QC → Blank → *randomised samples* → HeLa QC → Blank
- Seeded randomisation — record and reuse the random seed to reproduce an exact run order
- Configurable QC positions, injection volumes, file naming conventions
- 384-well plate map with click, rectangular drag (select or deselect mode), and paste-from-Excel well selection
- Sample condition summary grouped by replicate for quick QC of your experimental design

---

## 🖥️ Interface Overview

### Sidebar — Settings

| Section | What to fill in |
|---------|----------------|
| **Metadata File** | Upload the `.xlsx` from `plate_layout_gui.html`. Map columns for Well, Prep Finished, Experiment Name, Date. |
| **Run Settings** | Data path, instrument method path, short name, plate position, injection volume, batch label, run code, date/experiment overrides, LCMS method time (optional), random seed (optional) |
| **Blank / BSA QC / HeLa QC** | Name prefix, suffix/label, plate position, injection volume for each QC type |

### Main Panel — Well Selection

- **Click** a well to toggle it
- **Drag** on the background to rectangle-select (switch between ＋ Select / － Deselect mode with the toolbar buttons)
- **Paste TRUE/FALSE table** — paste a 16×24 tab-separated grid directly from Excel/Sheets; accepts `TRUE/FALSE`, `1/0`, or `YES/NO`
- Toolbar buttons: All Finished, All, Clear, Invert

### Preview Tabs (after Generate)

| Tab | Contents |
|-----|----------|
| **Table** | Full Xcalibur sequence row-by-row |
| **Summary** | Row counts, run order, est. run time (if method time set), random seed used |
| **Samples** | Grouped replicate table — conditions × replicate count, balance check, well list |

---

## 📤 Output Files

### Excel — `YYYYMMDD_expName_xcalibur_sequence.xlsx`

| Sheet | Contents |
|-------|----------|
| `Xcaliber_seqeunce` | Ready-to-import Xcalibur sequence (Bracket Type=4) |
| `wells_to_lcms` | Per-sample well → file name mapping with randomisation index |
| `Selected_Wells_384` | 16×24 plate grid of 1/0 — which wells were sent to LCMS |
| `Settings` | All run parameters, QC config, random seed |
| `Summary` | Row counts, run order, estimated run time |
| `Sample_Summary` | Condition groups × replicate counts — same as the Samples tab |

### CSV — `YYYYMMDD_expName_Xcaliber_seqeunce.csv`

Direct Xcalibur import file (same content as Sheet 1 of the Excel).

### Session — `YYYYMMDD_expName_xcaliber_generating_session.json`

Saves all settings, well selection, and the previously generated sequence. Load it back to restore everything exactly — including the sequence preview — without re-generating.

---

## 🗂️ Example Files

The `examples/` folder contains a working example you can try:

| File | Description |
|------|-------------|
| `20260101_example_metadata.xlsx` | Input metadata (from the plate layout GUI) |
| `20260101_example_xcaliber_generating_session.json` | Load this to restore the full example session |
| `20260101_example_xcalibur_sequence.xlsx` | Excel output generated from that session |
| `20260101_example_Xcaliber_seqeunce.csv` | CSV output generated from that session |

**To try the example:**
1. Open `xcalibur_sequence_generator.html`
2. Click **📂 Load Session** → select `20260101_example_xcaliber_generating_session.json`
3. Everything loads — settings, well selection, and the previously generated sequence

---

## 🔁 Reproducible Randomisation

Every time you click **▶ Generate**, the sample order is randomised using a seeded PRNG (mulberry32).

- If the **Randomization Seed** field is blank, a new random seed is generated and written back into the field
- The seed used is shown in the **Summary** tab and saved in the session JSON and XLSX Settings sheet
- To reproduce an exact run order: paste the seed back into the field and click Generate again
- Click **🎲 New seed** to pick a fresh random seed without generating

---

## 🛠️ Technical Notes

The tool is a self-contained HTML file. It uses:

| Library | Purpose | How it's loaded |
|---------|---------|-----------------|
| [SheetJS (xlsx)](https://sheetjs.com) | Excel file read/write | CDN |

No server, no Python, no `npm install` — everything runs in the browser.

---

## 🐛 Known Limitations

- Plate size is fixed at 384 wells (16 rows × 24 columns)
- Sequence structure is fixed: Blank → BSA → HeLa → Blank → samples → HeLa → Blank
- Requires internet connection on first open (CDN library)
- Designed for Thermo Xcalibur — file format may not be compatible with other instruments
