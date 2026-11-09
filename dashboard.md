# Looker Studio dashboard

> **Status: TO COMPLETE BEFORE SUBMITTING.** Build the dashboard in your own Google account, then replace the two placeholders below (the link and the screenshots). Delete this notice once done.

## Public link

**Dashboard:** `PASTE_YOUR_LOOKER_STUDIO_LINK_HERE`

Sharing must be set to **Anyone with the link can view** (Share > Manage access > General access). Test the link in a private/incognito window.

## Screenshots

Take at least two screenshots (full dashboard, plus one with a filter applied) and save them in a `screenshots/` folder.

![Dashboard overview: scorecards, trend and breakdowns](screenshots/dashboard_overview.png)

![Dashboard with the Branch drop-down and date range applied](screenshots/dashboard_filtered.png)

---

## Build guide (same story as the one-page report)

### 1. Connect the data
1. Go to [lookerstudio.google.com](https://lookerstudio.google.com) > **Create > Data source > File Upload**.
2. Upload `data/duka_sales_clean.csv`.
3. In the field list set the types:
   - `date_key` > **Date (YYYYMMDD)**, the date field used for the trend and the date-range control
   - `revenue`, `units`, `unit_price` > **Number** (currency: KES if offered)
   - everything else stays Text.
4. Add these **calculated fields**:

| Field name | Formula |
|---|---|
| Average order value | `SUM(revenue) / COUNT(order_id)` |
| Big-ticket revenue share | `SUM(CASE WHEN price_band = "Big-ticket" THEN revenue ELSE 0 END) / SUM(revenue)` |

### 2. Layout (top to bottom, mobile-friendly single column if possible)

| Block | Component | Setup |
|---|---|---|
| Title | Text | "Duka Electronics: H1 2026 sales" plus the Big Idea sentence |
| **Scorecard 1** | Scorecard | Metric: `SUM(revenue)`. Title: "H1 revenue (KES)" |
| **Scorecard 2** | Scorecard | Metric: `Record Count` (or `COUNT(order_id)`). Title: "Orders" |
| **Scorecard 3** | Scorecard | Metric: Average order value. Title: "Average order (KES)" |
| Scorecard 4 (optional) | Scorecard | Metric: Big-ticket revenue share (format as %). Title: "Big-ticket share of revenue" |
| **Monthly trend** | Time series | Date: `date_key`, granularity **Year Month**. Metric: `SUM(revenue)`. Title: "Monthly revenue (KES)" |
| **Breakdown 1** | Bar chart | Dimension: `product`. Metric: `SUM(revenue)`. Sort: revenue, descending. Title: "Revenue by product" |
| **Breakdown 2** | Bar chart | Dimension: `branch`. Metric: Average order value. Sort: descending. Title: "Average order by branch" |
| **Date control** | Date range control | Default range: 1 Jan to 30 Jun 2026 |
| **Drop-down control** | Drop-down list | Control field: `branch` (optionally add a second one on `channel`) |

### 3. Apply the same design rules as the report
- **One highlight colour** (`#E8590C`) and grey (`#B4B9C0`) for everything else. In the bar charts use **Style > Conditional/Single colour**, and set a single series colour to grey.
- Turn on **data labels**, turn off gridlines and legends, and sort bars descending.
- Write **insight titles** as sentences (for example "Three products earn 68% of revenue"), since Looker Studio titles are static text.
- Add a small text box at the bottom: "Source: Duka Electronics sales ledger, Jan-Jun 2026. KES = Kenya shillings."

### 4. Share
**Share > Manage access > General access > Anyone with the link > Viewer**. Copy the link into this file.

### Checklist (what the reviewer looks for)
- [ ] At least three KPI scorecards
- [ ] Monthly trend
- [ ] Two breakdowns (product and branch)
- [ ] Date-range control
- [ ] One drop-down control
- [ ] Link set to "Anyone with the link can view"
- [ ] At least two screenshots committed under `screenshots/`
