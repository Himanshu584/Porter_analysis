# Porter | Optimizing Delivery for the Digital Diner

### Excel · Power Query · PivotTables · Data Analytics · Interactive Dashboard

A food-delivery operations analytics case study exploring **where delivery delays occur**, how performance varies across markets and demand periods, and which operational improvements are worth investigating.

## Dashboard Preview

![Porter Delivery Analytics Dashboard]([Dashboard_Screenshot.png](https://github.com/Himanshu584/Porter_analysis/blob/main/dashboard_screenshot.png))



## At a Glance

| Metric | Result |
|---|---:|
| Source records | 197,428 |
| Deliveries with valid duration | **197,418** |
| Average delivery time | **47.69 min** |
| Delivered within 30 minutes | **13.16%** |
| Fastest valid delivery | **1.68 min** |
| Slowest valid delivery | **950.53 min** |

The **30-minute benchmark** is used for this project; it is not a verified contractual service-level target.

## Business Questions

- When does order demand peak, and how does delivery performance vary by hour and weekday?
- Which markets and restaurant categories have the greatest delivery-performance challenges?
- How is delivery-partner availability associated with delivery duration?
- Does order size relate to longer delivery times and lower 30-minute completion rates?

## Tools and Techniques

- **Microsoft Excel:** PivotTables, PivotCharts, combo charts, doughnut charts, KPI cards, slicers, and linked dashboard calculations.
- **Power Query:** Data typing, missing-value handling, duration calculations, conditional columns, and data-quality flags.
- **Descriptive analytics:** Segmentation, volume comparisons, average delivery duration, and 30-minute completion rates.

## Data Preparation

The source CSV contains **197,428 records**. Key transformations include:

1. Calculated `Delivery_Minutes` from order creation and actual delivery timestamps.
2. Classified durations as `Valid`, `Missing`, `Invalid`, or `Extreme` (over 24 hours).
3. Created `Within_30_Min`, `Order_Hour`, `Order_Day`, and `Order_Size_Group` fields.
4. Calculated partner availability only when on-shift and busy-partner counts were present and internally consistent.
5. Retained records with missing or inconsistent partner data for unrelated analyses, excluding them **only** from partner-availability comparisons.

**Analysis populations:** 197,418 valid-duration deliveries for the main performance analysis; **140,743** records with both valid duration and valid partner availability for the partner-efficiency analysis.

## Key Findings

### 1. Demand peaks align with slower deliveries

- The busiest recorded hour was **02:00**, with **36,972 orders**, an average delivery time of **54.84 min**, and a **4.15%** within-30-minute rate.
- **Saturday** had the highest weekday volume (**34,541 orders**).
- **Monday** had the slowest weekday average (**51.51 min**), while **Wednesday** was fastest (**44.22 min**).

*The source timezone has not been independently verified; recorded hours should not be assumed to be local restaurant time.*

### 2. Market 1 merits operational investigation

- **Market 1:** 38,035 deliveries, **51.33 min** average, **11.70%** within 30 minutes.
- **Market 2:** 55,055 deliveries, **46.07 min** average—the highest-volume and fastest-average market in the analysis.

Market labels are anonymized IDs, not verified city names.

### 3. Pizza is a high-volume category with slower deliveries

- **Pizza:** 17,320 orders, **50.87 min** average, **7.94%** within 30 minutes.
- **Mexican:** 17,098 orders, **44.55 min** average, **17.68%** within 30 minutes.

These differences warrant further investigation; the dataset does not isolate restaurant preparation time or delivery distance.

### 4. Zero available partners is associated with slower deliveries

| Available partners | Deliveries | Avg delivery time | Within 30 min |
|---|---:|---:|---:|
| 0 | 35,909 | **52.35 min** | 8.66% |
| 1–5 | 56,967 | 46.43 min | 14.44% |
| 6–10 | 21,393 | 44.23 min | **17.17%** |
| 11–20 | 16,554 | **44.06 min** | 16.30% |
| 21+ | 9,920 | 45.95 min | 10.05% |

The difference between the zero-available and 11–20-available groups is **8.29 minutes** on average. This is an **association, not evidence of causation**.

### 5. Larger orders tend to take longer

| Order size | Deliveries | Avg delivery time | Within 30 min | Avg subtotal* |
|---|---:|---:|---:|---:|
| 1–2 items | 95,750 | 45.58 min | 16.68% | 1,726.81 |
| 3–5 items | 78,440 | 48.72 min | 10.73% | 3,108.93 |
| 6+ items | 23,228 | **52.93 min** | **6.84%** | 5,180.53 |

Orders with six or more items averaged **7.35 minutes longer** than orders with one or two items.

*Subtotal units/currency were not independently verified.*

## Dashboard Features

The Excel dashboard includes:

- **5 KPI cards:** valid deliveries, average delivery time, 30-minute completion rate, fastest delivery, and slowest delivery.
- **6 charts:** hourly demand, weekday delivery time, market comparison, partner availability, order-size performance, and order-size distribution.
- **Market ID slicer:** interactive filtering of connected PivotTables and dashboard components.

## Recommendations

1. **Investigate courier supply gaps:** examine zero-availability periods by market and hour before piloting targeted dispatch or staffing changes.
2. **Prioritize Market 1 diagnostics:** segment its performance by hour, restaurant category, order size, and courier availability.
3. **Review pizza-order workflows:** compare preparation and pickup processes against faster high-volume categories.
4. **Refine large-order delivery estimates:** test whether order-size-aware estimates improve customer-facing reliability.
5. **Measure impact carefully:** track average and median delivery time, the 30-minute rate, and upper-tail delays before and after operational pilots.

## Project Files

```text
Porter-Delivery-Analytics/
├── README.md
├── Porter_Delivery_Analysis.xlsx
├── Porter_Business_Case_Study.docx
├── Porter_Solution_Guide.docx
└── Dashboard_Screenshot.png
```

- **[Excel analysis and dashboard](Porter_Delivery_Analysis.xlsx)** — cleaned dataset, PivotTables, and interactive dashboard.
- **[Business case study](Porter_Business_Case_Study.docx)** — business context, findings, and recommendations.
- **[Solution guide](Porter_Solution_Guide.docx)** — transformations, analytical methodology, and dashboard setup.

## How to Explore

1. Download `Porter_Delivery_Analysis.xlsx` and open it in **Microsoft Excel desktop**.
2. Open the **Dashboard** worksheet.
3. Use the **Market ID** slicer to compare markets; clear the slicer to restore the overall view.
4. Inspect the **Analysis** worksheet for the supporting PivotTables.
5. If refreshing data, preserve the expected source-file location and use **Data → Refresh All**.

## Limitations

- Findings are **descriptive**, not causal; traffic, distance, weather, and detailed preparation timestamps were not available.
- The recorded timestamp **timezone is unverified**.
- Duration filtering removes missing, nonpositive, and over-24-hour values but retains some unusually long deliveries.
- Partner availability analysis excludes missing or internally inconsistent partner counts.
- The 30-minute threshold is an analytical benchmark, not a confirmed company SLA.

---

**Project focus:** Turning raw operational data into a reproducible Excel dashboard and evidence-based delivery optimization hypotheses.
