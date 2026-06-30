# Exchange Public Disclosure Portal

A single-page web app for browsing SEBI regulatory bulletin data, IPO/Buyback corporate actions, a live market radar, and a stock screener — all rendered client-side from Excel workbooks hosted on GitHub.

## What it does

- **Historical Data** — reads `PRASAD_INDEX_FILE.xlsx` to build a category/table index, then pulls the matching sheet from the Annual, Monthly, or Daily bulletin workbook depending on the frequency selected.
- **Investor Corner** — Stock Screener, IPO Segment (Upcoming/Recent/Below Issue Price/Rights), and Buyback/Tender/Delisting tracker, each reading from their own workbook.
- **Live Market Radar** — index and sector performance views, Top Gainers/Losers, and most active stocks.
- All tables are client-side sortable, with pagination or a "view full dataset" popup where relevant, and wide tables scroll horizontally inside their own container rather than stretching the page.

## How it works

The page has no backend. On load, it fetches `.xlsx` files directly from this repository's raw GitHub URLs and parses them in the browser with [SheetJS](https://sheetjs.com/). Charting uses [Chart.js](https://www.chartjs.org/), icons use [Lucide](https://lucide.dev/), and styling uses [Tailwind CSS](https://tailwindcss.com/) (all loaded via CDN — no build step).

## Data sources

The app expects these workbooks to be reachable at `https://raw.githubusercontent.com/<owner>/<repo>/<branch>/files/`:

| File | Used for |
|---|---|
| `PRASAD_INDEX_FILE.xlsx` | Category → table → sheet index for Historical Data |
| `PRASAD_BULLETIN_FILES_ANNUAL.xlsx` | Annual frequency bulletin tables |
| `PRASAD_BULLETIN_FILES_MONTHLY.xlsx` | Monthly frequency bulletin tables |
| `PRASAD_BULLETIN_DAILY.xlsx` | Daily/granular bulletin tables |
| `IPO_Segment.xlsx` | IPO Segment tabs |
| `buyback.xlsx` | Buyback / Tender Offer / Delisting Offer tabs |

If these files live in a different repository or branch than this one, update the `GITHUB_BASE` and `GITHUB_FILES` constants near the top of the `<script>` block in `Unified_Data_Reporting_v3.html`.

## Viewing it live

Once pushed to GitHub, you can serve this file for free with **GitHub Pages**: repo Settings → Pages → Deploy from branch → select `main` → save. GitHub Pages looks for `index.html` by default, so either rename `Unified_Data_Reporting_v3.html` to `index.html`, or set the Pages source to serve this specific file.

## Local preview

No install needed — just open `Unified_Data_Reporting_v3.html` directly in a browser. (Live data still loads from GitHub, so you'll need an internet connection.)
# stock_data
