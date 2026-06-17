# Supply Chain Performance Analytics — Multi-Facility Distribution Network

**Tools:** Python · Power BI · Prophet  
**Dataset:** DataCo Smart Supply Chain (180K+ records, filtered to 10,960 US orders)  
**Skills:** Data Cleaning · Exploratory Analysis · Dashboard Design · Demand Forecasting

---

## Business Problem

More than half of all orders processed across a two-facility US distribution network arrive late. This project analyzes **10,960 orders** across two distribution centers — Jacksonville, FL (Southeast) and Bethlehem, PA (Northeast), to answer three operational questions:

1. What does current network performance look like at the executive level?
2. Which facility is underperforming, and why?
3. What is actually driving the late delivery problem — and what should be done about it?

---

## Key Findings

### 55.7% of orders arrive late — and it's not a facility problem

Both Jacksonville (55.77% late rate) and Bethlehem (55.66% late rate) produce nearly identical late delivery rates despite Bethlehem handling 71% more order volume (6,915 vs. 4,045 orders). When two facilities with dramatically different volumes produce the same late rate, the root cause is **systemic and network-wide**, not site-specific. A facility-level operational fix would not solve this.

### First Class shipping has a 95.97% late delivery rate

The premium shipping tier, meaning the option customers pay more for expecting faster, more reliable delivery, is the worst-performing mode in the network by a wide margin:

| Shipping Mode | Late Rate |
|---|---|
| First Class | **95.97%** |
| Second Class | 77.31% |
| Same Day | 45.94% |
| Standard Class | 39.24% |

The heatmap analysis confirms this is universal across every product category — it is a shipping mode failure, not a category-specific issue. The most likely root causes are carrier performance failure for First Class routes in these regions, or promise dates set more aggressively than carrier lead times allow.

### Demand is forecast to grow ~57% over the next 90 days

A Prophet time series model trained on five months of daily order volume projects demand growing from ~70 orders/day to ~110 orders/day by late November. A network already failing more than half its orders at current volume will face compounding operational pressure as demand scales.

---

## Recommendations

**1. Network-level intervention, not a facility fix.**  
Address carrier contracts, shipping mode assignment policy, or promise date methodology at the network level. A site-by-site operational effort will not move the needle when both facilities are producing identical late rates.

**2. Investigate First Class immediately.**  
A 96% late rate on a premium product is both an operational failure and a customer trust issue. Priority investigation areas: carrier-level performance data for First Class routes, promise date methodology vs. actual carrier commitments, and pick-and-pack prioritization by shipping mode.

**3. Fix the problem before volume peaks.**  
The 90-day demand forecast creates urgency. Addressing staffing, carrier capacity, and shipping mode allocation now — at current volume — is significantly more cost-effective than attempting to fix a broken network under peak operational load.

---

## Project Structure
├── supply_chain_analysis.ipynb  # Data cleaning, feature engineering, and Prophet demand forecast

├── dashboard/                   # Power BI (.pbix) file — 3-page interactive dashboard

└── README.md

### Notebook Overview

The Jupyter notebook covers the full analytical pipeline:

- **Data quality assessment** — identified and dropped 6 non-informative columns (100% null, single-value, URL-only fields)
- **Date parsing** — converted string timestamps to proper datetime objects for time-based analysis
- **Feature engineering** — created `Fulfillment Gap` (actual vs. scheduled shipping days) and `Is Late` binary flag
- **Facility mapping** — derived Jacksonville and Bethlehem assignments from order region data
- **Prophet demand forecast** — 90-day forward projection with confidence intervals, capturing weekly seasonality and upward trend

### Dashboard Overview

Three-page Power BI dashboard with interactive slicers (facility, month, shipping mode):

- **Executive Summary** — KPI cards, monthly order volume trend, order status breakdown, top product categories
<img width="956" height="533" alt="image" src="https://github.com/user-attachments/assets/e002513d-a231-4c26-9f61-4814a5ffd70a" />

- **Facility Comparison** — side-by-side JAX vs. BTH on late rate, volume, fulfillment gap, and shipping mode performance
<img width="1007" height="562" alt="image" src="https://github.com/user-attachments/assets/19721148-178c-45da-8da2-9cfc32ee1db9" />

- **Operational Insights** — late rate by shipping mode, fulfillment gap distribution, category × shipping mode heatmap
<img width="956" height="536" alt="image" src="https://github.com/user-attachments/assets/5ae43334-96bc-4565-8062-d0e3f93390e9" />

---

## Data Source

[DataCo Smart Supply Chain Dataset](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis) — 180,519 order records covering global supply chain operations. Analysis filtered to US/Canada market reflecting North American distribution context.

---

## About

Built as a portfolio project demonstrating end-to-end supply chain analytics; from raw data to executive-ready insights. The analysis mirrors real operational questions a Business/Data Analyst would face in a multi-facility distribution environment.

**Luis Fabian Cuevas Martinez** · [Portfolio](https://luiscuevasportfolio.netlify.app) · [GitHub](https://github.com/LuisCuevasData)
