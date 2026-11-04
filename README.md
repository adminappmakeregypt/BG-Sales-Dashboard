# Alborg Scan Business Review Dashboard

A static dashboard (HTML, CSS and JavaScript) for the monthly Alborg Scan business review. It reads an Excel workbook directly in the browser, so it needs no server and no build step.

## Pages

| # | Page | Data sheet(s) |
|---|------|---------------|
| 1 | Network overview: branches vs target and last year | `Branch_KPI` |
| 2 | Modality performance: per exam type, YoY and MoM | `Modality_KPI` (or `Branch_Modality` when a branch is selected) |
| 3 | Machine utilization: heatmap, weekly trend, spare capacity | `Utilization` |
| 4 | Branch deep-dive: one branch, per modality | `Branch_Modality`, `Branch_History` |
| 5 | Doctors & medical reps: scorecard, specialties, movers, feedback | `Rep_KPI`, `Specialty_Branch`, `Doctor_YoY`, `Doctor_Summary`, `Doctor_Feedback` |
| 6 | Corporate analysis: categories and top customers | `Corp_Category`, `Corp_Customers` |

## Filters

- **From / To month** and **Quick range** (latest month, year to date, all). Rows are summed across the selected months.
- **Branch** and **Segment** (walk-in / corporate) apply wherever the data has those columns. A note on the page says when they don't.
- Each page also has its own filters: metric, modality, rep, specialty, reason, customer category and others.
- Every table supports sorting (click a header), searching, and **CSV export**.

## Presenting

- **▶ Present** switches to full screen with bigger charts. Use the **← / →** keys to move between pages.
- **◐ Theme** toggles light and dark. **⎙ Print** prints the current page.
- You can link straight to a page, e.g. `.../index.html#utilization`.

## Publish on GitHub Pages

1. Create a repository, e.g. `bgscan-dashboard`.
2. Upload this folder's contents, keeping the structure:
   ```
   index.html
   css/styles.css
   js/app.js
   data/BG_Scan_Dashboard_Data.xlsx   (optional: auto-loads on open)
   README.md
   ```
3. Go to **Settings → Pages → Build and deployment**, choose **Deploy from a branch**, select `main` and the `/ (root)` folder, then **Save**.
4. After about a minute the site is live at `https://<your-user>.github.io/bgscan-dashboard/`.

> **Confidentiality:** a public repository makes the data file public. If the workbook holds internal figures, either leave it out of `data/` (users then upload it in the browser, and it never leaves their machine) or use a private repository with Pages restricted to your organisation.

## Monthly update

1. Open `BG_Scan_Dashboard_Data.xlsx`.
2. Append the new month's rows to each sheet with a new **Period** (the first day of the month, e.g. `01/11/2026`). Keep the column names unchanged; the formula columns at the right can be left empty.
3. Either upload the file with **⤒ Upload Excel** (or drag it onto the page), or replace `data/BG_Scan_Dashboard_Data.xlsx` in the repository.

If a sheet or required column is missing, the dashboard shows a "Workbook check" notice instead of failing.

## Settings

The thresholds are at the top of `js/app.js`:

```js
const ACH_GOOD = 1.0;   // ≥100% of target = green ✓
const ACH_WARN = 0.85;  // 85–99% = amber ▲, below = red ▼
const UTIL_HIGH = 0.9;  // utilization treated as capacity-constrained
```

## Libraries (loaded from cdnjs)

- SheetJS `xlsx` 0.18.5 for reading Excel
- Chart.js 4.4.1 for charts
