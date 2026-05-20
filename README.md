# Pivot Tables Unit — AP Computer Science A

A three-day data unit for AP Computer Science A at Divine Child High School. Students learn pivot tables in Google Sheets using a 500-record Michigan traffic crash dataset, then submit their work as a PDF.

**Live site:** _enable GitHub Pages and put the URL here_

## What's in the unit

| Day | Topic | Skills |
|-----|-------|--------|
| 1 | Introduction from scratch | Rows, Values, the COUNTA/SUM aggregation |
| 2 | Filters & cross-tabs | Filtering before aggregation, two-dimensional grouping |
| 3 | Visualizing | Bar / stacked-bar / line charts from pivots |

Each day is a single self-contained HTML page with a built-in PDF generator. Students enter their name, click **Download PDF & Submit**, and upload the resulting PDF to Google Classroom.

## Repo layout

```
pivot-tables-unit/
├── index.html              # Landing page linking to all three days
├── day1.html               # Day 1 — Introduction
├── day2.html               # Day 2 — Filters & Cross-tabs
├── day3.html               # Day 3 — Visualizing
├── data/
│   ├── michigan_crashes.csv   # 500-row dataset (the single source of truth)
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
- All three days reference the **same 500-row dataset**. Update `data/michigan_crashes.csv` once and re-run `build_data.mjs` (kept in this repo's history) if you ever change it.

The only external dependency is Google Fonts (for Fraunces / DM Sans / DM Mono). If the school blocks Google Fonts, the pages fall back to system fonts and still work.

## Submit / PDF flow

On each day's last section students:

1. Enter their name in the **Your name** field
2. Click **Download PDF & Submit**
3. Browser downloads `PivotTables_DayN_FirstName_LastName.pdf` with every answer they typed

The PDF includes a cover page, every section's responses, and a footer with student name and class identifier. No data leaves the browser — generation is 100% client-side.

## Local development

Open `index.html` directly in a browser, or for a tiny local server:

```bash
cd pivot-tables-unit
python3 -m http.server 8000
# then visit http://localhost:8000
```

---

*AP CS A · Divine Child High School*
