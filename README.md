# Car Sales Analytics Dashboard | Power BI

**From raw automotive sales data to actionable business insights.**

An end-to-end Business Intelligence project analyzing approximately 559,000 vehicle sales transactions and $7.61 billion in sales revenue across the US automotive market (2014–2015).

The project covers Power Query ETL, dimensional data modeling, advanced DAX calculations, and interactive dashboard development.

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?logo=powerbi&logoColor=black)
![Power Query](https://img.shields.io/badge/Power%20Query-ETL-217346)
![DAX](https://img.shields.io/badge/DAX-Advanced-0078D4)
![Transactions](https://img.shields.io/badge/Transactions-559K-1E2761)
![Revenue](https://img.shields.io/badge/Revenue-$7.61B-97BC62)

---

## Business Problem

Raw automotive transaction data made it difficult to evaluate sales performance, compare manufacturers, assess market pricing, and monitor seller contributions.

The dashboard was developed to answer four key business questions:

- Which manufacturers, models, and geographic markets generate the most revenue?
- How do vehicle mileage and condition relate to selling prices?
- Are vehicles being sold above or below their market reference values?
- Which sellers drive revenue, and how concentrated is sales performance?

---

## Key Metrics

| Metric | Value |
|---|---:|
| Total Revenue | $7.61B |
| Total Cars Sold | ~559,000 |
| Average Selling Price | $13,610 |
| Price vs. MMR | -1.15% |
| Pricing Efficiency | 98.9% |
| Average Mileage | 68,320 mi |
| Average Condition Score | 30.67 |
| Top 10 Seller Revenue Share | 26.0% |

---

## Key Business Insights

- **Manufacturer performance:** Ford leads the market with $1.36B in revenue, followed by Chevrolet ($723.37M) and Nissan ($633.70M).
- **Sales performance:** February 2015 recorded the highest monthly revenue ($2.2B) and sales volume (163K vehicles).
- **Pricing performance:** Vehicles were sold approximately 1.15% below their MMR market reference value.
- **Mileage impact:** Average selling prices decrease from approximately $21K for vehicles below 20K miles to $6K for vehicles with 80K+ miles.
- **Transmission preference:** Automatic vehicles account for 85.2% of total sales volume.
- **Seller concentration:** The top 10 sellers generate 26% of total revenue, with Ford Motor Credit Company leading at $340.96M.
- **Model performance:** BMW generated $446.51M from 20,793 vehicles, with the 3 Series contributing 30.89% of BMW's revenue.

---

## Dashboard Preview

### Page 1 — Executive Overview

![Executive Overview](images/overview.png)

A consolidated view of revenue, sales volume, market pricing, monthly trends, vehicle segments, transmission distribution, and geographic performance.

**Key features:** KPI cards with sparklines, dynamic metric switching, year selection, and geographic shape map.

### Page 2 — Sales Deep Dive

![Sales Deep Dive](images/sales-deep-dive.png)

Detailed analysis of manufacturer performance, vehicle mileage, condition, and pricing efficiency.

**Key features:** Dynamic Top 5/10/15 manufacturers, market price gap analysis, mileage segmentation, and a decomposition tree for exploring revenue drivers.

### Page 3 — Seller Performance

![Seller Performance](images/seller-performance.png)

Seller benchmarking based on revenue, sales volume, pricing efficiency, and revenue concentration.

**Key features:** Top 10 seller ranking, conditional formatting, detailed performance matrix, and monthly revenue versus sales volume analysis.

### Page 4 — Make Performance (Drill-through)

![Make Performance](images/make-performance.png)

Manufacturer-specific analysis with model-level revenue, sales volume, market pricing, and vehicle condition distribution.

**Key features:** Dynamic manufacturer logo and title, Top 3/5/10 model rankings, revenue contribution analysis, and dynamic business insight text.

---

## Data Preparation & ETL

The original CSV dataset contains 16 fields covering vehicle characteristics, transaction prices, market reference values, seller information, and sale dates.

Data cleaning and transformation were performed using **Power Query and M Language**.

| Data Quality Issue | Transformation |
|---|---|
| Missing categorical values | Standardized as UNKNOWN |
| Extra spaces and invalid characters | Text.Trim and Text.Clean |
| Inconsistent manufacturer names | Text.Upper |
| Invalid color and interior values | Placeholder standardization |
| Incorrect numeric data types | Safe conversion using try...otherwise |
| Unstructured sale dates | Date parsing and conversion |
| Invalid transactions | Removed invalid dates and non-positive prices |

Additional analytical attributes were created for vehicle age, mileage bands, condition categories, and geographic segmentation.

---

## Data Model

The semantic model follows a fact-and-dimension architecture.

| Table | Purpose |
|---|---|
| FactSales | Cleaned automotive sales transactions |
| DimDate | Calendar and time intelligence |
| DimMake | Manufacturer-level analysis |
| DimSeller | Seller-level analysis |
| Logos | Dynamic manufacturer images |
| AllMeasure | Centralized DAX measures |

Additional parameter tables support dynamic rankings, metric switching, and analytical segmentation.

```mermaid
flowchart LR
    A[Raw CSV] --> B[Power Query ETL]
    B --> C[Data Model]
    C --> D[DAX Measures]
    D --> E[Interactive Dashboard]
```

---

## DAX Implementation

Reusable DAX measures were developed for revenue, sales volume, time intelligence, pricing performance, dynamic rankings, and contribution analysis.

### Revenue YoY Growth

```dax
Revenue YoY % =
VAR CurrentRevenue = [Total Revenue]
VAR PreviousRevenue = [PY Revenue]
RETURN
IF(
    ISBLANK(PreviousRevenue) ||
    PreviousRevenue = 0,
    BLANK(),
    DIVIDE(
        CurrentRevenue - PreviousRevenue,
        PreviousRevenue
    )
)
```

### Model Revenue Contribution

```dax
Model Revenue Share % =
DIVIDE(
    [Total Revenue],
    CALCULATE(
        [Total Revenue],
        ALLSELECTED(FactSales[model])
    )
)
```

Other analytical techniques include CALCULATE, RANKX, DIVIDE, time intelligence functions, dynamic Top N filtering, and filter context management.

---

## Interactive Features

- Bookmark-based filter panels and reset buttons
- Page navigation and drill-through
- Dynamic Top N rankings
- Field parameters and metric switching
- Custom report page tooltips
- Dynamic titles, logos, and business insights
- Conditional KPI and matrix formatting
- Chiclet Slicer custom visual
- Revenue decomposition tree

---

## Skills Demonstrated

| Skill | Application |
|---|---|
| Power Query & M Language | Data cleaning, transformation, and validation |
| Data Modeling | Fact and dimension architecture |
| DAX | KPIs, time intelligence, rankings, and filter context |
| Business Analytics | Sales, pricing, and seller performance |
| Data Visualization | Interactive and business-oriented reporting |
| Dashboard UX/UI | Bookmarks, navigation, filters, and drill-through |
| Data Storytelling | Translating analytical results into business insights |

---

## Repository Structure

```text
Car-Sales-Analytics-PowerBI/
├── README.md
├── CarSales.pbit
└── images/
    ├── overview.png
    ├── sales-deep-dive.png
    ├── seller-performance.png
    └── make-performance.png
```

## How to Open

1. Download CarSales.pbit from this repository.
2. Open the template with Microsoft Power BI Desktop.
3. Obtain the original car_prices.csv dataset.
4. Update the CSV source path in Power Query.
5. Apply changes and refresh the report.

**Note:** The original dataset is not included due to GitHub's browser upload file-size limit. The PBIT template contains the report design, Power Query transformations, data model, and DAX calculations.

## Analytical Limitations

- MMR represents a market reference value, not vehicle acquisition cost. Pricing deviation should not be interpreted as profit.
- Historical data coverage is uneven across 2014–2015, which limits the reliability of year-over-year comparisons.
- Mileage and pricing relationships are descriptive and do not establish causation.

---

## Author

**Javohir Yunusov**

Data Analyst | SQL · Python · Power BI

[LinkedIn](https://www.linkedin.com/in/javohir-yunusov-705424295) · [Telegram](https://t.me/yunusovv66)

> Developed as an academic final project and professional Business Intelligence portfolio project.
