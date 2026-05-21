# Pivot Tables Unit — AP Computer Science A

A four-day data unit for AP Computer Science A at Divine Child High School. Students learn pivot tables in Google Sheets using a 500-record Michigan traffic crash dataset, then cap the unit with a week-long mini-project on a dataset of their choice.

**Live site:** [https://github.com/falconphysics/PivotTables](https://github.com/falconphysics/PivotTables)

## What's in the unit

| Day | Topic | Skills |
|-----|-------|--------|
| 1 | Introduction from scratch | Rows, Values, the COUNTA/SUM aggregation |
| 2 | Filters & cross-tabs | Filtering before aggregation, two-dimensional grouping |
| 3 | Visualizing | Bar / stacked-bar / line charts from pivots |
| 4 | Mini-project (week-long) | Choose a dataset, frame a question, analyze, present |

Days 1–3 are single-class lessons. Each is a self-contained HTML page with a built-in PDF generator — students enter their name, click **Download PDF & Submit**, and upload the resulting PDF to Google Classroom.

Day 4 is a week-long capstone. Students pick from a curated list of datasets (Kaggle, data.gov) or bring their own that meets the criteria, then work through dataset selection, question framing, iterative analysis with pivot logs, and presentation planning. The page auto-saves their progress to localStorage so they can return to it across the week. Final deliverable is the PDF plus a 3-minute in-class presentation.

## Repo layout

```
pivot-tables-unit/
├── index.html              # Landing page linking to all four days
├── day1.html               # Day 1 — Introduction
├── day2.html               # Day 2 — Filters & Cross-tabs
├── day3.html               # Day 3 — Visualizing
├── day4.html               # Day 4 — Mini-Project (week-long capstone)
├── data/
│   ├── michigan_crashes.csv   # 500-row dataset (used by Days 1–3)
│   └── michigan_crashes.js    # Same data as JS for offline use
└── vendor/
    ├── jspdf.umd.min.js       # Vendored — PDF generation
    └── chart.umd.min.js       # Vendored — Day 3 charts
```

## Deploying as a GitHub Page

1. Create a new repository on GitHub (e.g. `pivot-tables-unit`). Make it **public**.
2. Push this folder's contents to `main`:
   ```bash
   cd pivot-tables-unit
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/<your-username>/pivot-tables-unit.git
   git push -u origin main
   ```
3. On GitHub: **Settings → Pages → Source: Deploy from a branch → Branch: main, folder: / (root) → Save**.
4. After ~1 minute, GitHub gives you a URL like `https://<your-username>.github.io/pivot-tables-unit/`. Share that link in Schoology.

## Why everything is self-contained

The school network may block CDNs, and Schoology has been known to strip `<script>` tags inside embedded HTML. To avoid both problems:

- jsPDF and Chart.js are **vendored locally** in `vendor/`. No CDN dependency at runtime.
- The dataset is **embedded as `data/michigan_crashes.js`** so the pages work even when loaded over `file://` (no `fetch` calls).
- Days 1–3 reference the **same 500-row dataset**. Update `data/michigan_crashes.csv` once and re-run `build_data.mjs` (kept in this repo's history) if you ever change it.
- Day 4 uses **localStorage** to persist student work across the week. Each browser keeps its own copy under the key `pivotTables_day4_v1` — no data leaves the device.

The only external dependency is Google Fonts (for Fraunces / DM Sans / DM Mono). If the school blocks Google Fonts, the pages fall back to system fonts and still work.

## Submit / PDF flow

On each day's last section students:

1. Enter their name in the **Your name** field
2. Click **Download PDF & Submit**
3. Browser downloads `PivotTables_DayN_FirstName_LastName.pdf` with every answer they typed

The PDF includes a cover page, every section's responses, and a footer with student name and class identifier. No data leaves the browser — generation is 100% client-side.

For Day 4, students also bring a 3-minute presentation (slide deck or poster) to class on the final day. The PDF captures their dataset choice, three candidate questions, pivot log of attempts, finding, and talking points — enough that you can review their thinking before they present.

## Local development

Open `index.html` directly in a browser, or for a tiny local server:

```bash
cd pivot-tables-unit
python3 -m http.server 8000
# then visit http://localhost:8000
```

---

*AP CS A · Divine Child High School*
