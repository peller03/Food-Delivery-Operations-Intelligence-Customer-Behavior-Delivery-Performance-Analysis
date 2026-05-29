# Food Delivery Operations Intelligence — Customer Behavior & Delivery Performance Analysis

---

## Table of Contents
- [Project Scope](#project-scope)
- [Data Sources](#data-sources)
- [Tool Used](#tool-used)
- [Data Cleaning & Preparation](#data-cleaning--preparation)
- [Exploratory Data Analysis Performed](#exploratory-data-analysis-performed)
- [EDA Visual Insights](#eda-visual-insights)
- [Data Analysis](#data-analysis)
- [Results / Findings](#results--findings)
- [Recommendations](#recommendations)
 

---

## Project Scope

This project analyzes a **food delivery operations dataset containing 72,314 delivery orders across customers, restaurants, drivers, and delivery areas** to uncover operational bottlenecks, customer ordering behavior, revenue retention patterns, and delivery performance inefficiencies affecting customer experience.

The objective of the analysis is to transform raw delivery activity into **operational intelligence** by identifying where delays occur in the delivery pipeline, how customer demand changes across time periods, which operational stages slow fulfillment, and how refunds, discounts, and service inefficiencies affect actual retained revenue.

Rather than focusing only on sales performance, the project evaluates how operational execution directly influences customer satisfaction, delivery reliability, and long-term business sustainability.

The analysis is structured into **three analytical dashboards**:

- **Executive Overview** — High level operational KPIs and delivery performance summary
- **Customer Behavior & Revenue** — Customer demand patterns, spending behavior, and revenue intelligence
- **Delivery Performance & Operational Efficiency** — Delivery timing analysis, delay monitoring, and process bottleneck identification

The dashboard focuses on answering key operational questions such as:

- Which days generate the highest customer demand and revenue?
- How does preparation time affect order volume?
- What percentage of deliveries are completed on time?
- Which operational stage contributes most to delays?
- How do refunds and discounts impact retained revenue?
- Are delivery inefficiencies concentrated during specific hours?
- Which delivery areas generate the strongest operational performance?
- How does customer urgency behavior influence delivery demand?

This approach demonstrates how delivery transaction data can evolve from simple order tracking into **actionable operational intelligence** capable of supporting logistics optimization and customer experience improvement.

---

## Dashboard Preview

  <img width="2075" height="3632" alt="Combined" src="https://github.com/user-attachments/assets/d807aed9-ad37-49e0-a676-83d207b86434" />

---

## Data Sources

The dataset used for this project consists of multiple operational and transactional variables representing the complete food delivery workflow.

### Core Operational Dataset
The primary dataset contains:

- Order ID
- Customer ID
- Driver ID
- Restaurant ID
- Delivery Area
- Order Time
- Restaurant Acceptance Time
- Driver Arrival Time
- Delivery Completion Time
- ASAP Order Status
- Sub Total
- Delivery Fee
- Service Fee
- Tip Amount
- Discount Amount
- Refunded Amount

The dataset captures the full lifecycle of a delivery order from customer placement through restaurant preparation and final delivery completion.

---

## Tool Used

- **Microsoft Power BI** — Dashboard development, DAX measures, and operational visualization
- **Power Query** — Data cleaning, time transformation, and feature engineering
- **Microsoft Excel** — Initial data inspection and preprocessing

---

## Data Cleaning & Preparation

The dataset required multiple preprocessing and transformation steps before operational analysis could be performed.

1. Built a **Calendar table** in Power BI to enable time intelligence analysis including Month Name, Week Day, Hour, and Weekly trend analysis.

2. Converted operational timestamp columns into proper datetime format for accurate delivery duration calculations.

3. Created custom operational KPIs including:
   - Delivery Time
   - Preparation Time
   - Driver Delay Time
   - On-Time Delivery Rate
   - Delay Rate

4. Created an **Order Hour** column to analyze customer demand concentration across hourly periods and identify peak operational pressure windows.

5. Developed a **Preparation Category** grouping classifying orders into:
   - Fast
   - Normal
   - Delayed
   - Slow

6. Applied operational duration calculations using DAX to measure:
   - Order to Restaurant Duration
   - Restaurant Preparation Duration
   - Driver Arrival Delay
   - Delivery Completion Duration

7. Built a **Net Revenue** measure representing actual retained business value after accounting for discounts and refunded amounts.

8. Handled blank timestamp values and validated time sequencing to avoid negative delivery duration calculations.

9. Applied “Sort by Column” for Month Name and Week Day fields to preserve correct chronological visual ordering.

10. Created KPI logic using **Flip Logic interpretation** where increases in operational delays and refunds are treated as negative business outcomes rather than automatically positive growth indicators.

These preprocessing steps ensured the dataset was operationally reliable and suitable for meaningful logistics and customer behavior analysis.

---

## Exploratory Data Analysis Performed

The EDA focused on understanding customer demand behavior, operational timing efficiency, delivery bottlenecks, and revenue retention performance.

### Executive Level KPIs
- Total Orders
- Total Customers
- Total Restaurants
- Total Drivers
- Gross Order Value
- Net Revenue
- Total Delivery Fees
- Total Discounts
- Total Refunds
- On-Time Delivery Rate
- Delay Rate

### Customer & Revenue KPIs
- Average Order Value
- Customer Distribution by Delivery Area
- Weekly Revenue Trend
- Tip Contribution Analysis
- Refund Impact on Revenue
- Revenue by Delivery Area
- ASAP Order Percentage
- Customer Order Frequency

### Operational Efficiency KPIs
- Average Delivery Time
- Average Preparation Time
- Average Driver Delay
- Delivery Delay Distribution
- Peak Delay Hours
- Hourly Order Heatmap
- Weekly Operational Performance
- Preparation Time Category Distribution
- On-Time vs Delayed Order Rate

These metrics collectively evaluate how operational performance influences customer satisfaction, demand retention, and overall delivery reliability.

---

## EDA Visual Insights

Key operational and behavioral insights observed during the analysis include:

- **Wednesday records both the highest order volume and highest revenue generation** across the entire week — indicating it is the strongest operational day for the business.

- **Wednesday also carries the lowest average preparation time at approximately 47 minutes** confirming that faster restaurant execution directly contributes to increased customer demand and transaction volume.

- **Less than half of all orders are delivered on time with an overall on-time delivery rate of 47.43%** revealing major operational inefficiencies across the delivery pipeline.

- **Average delivery completion time stands at 2 hours 18 minutes** significantly exceeding standard customer expectations for food delivery fulfillment.

- **Driver delay averages 55 minutes** indicating that operational slowdowns begin before final delivery execution, particularly during restaurant-driver coordination stages.

- **Preparation time averages 54 minutes** suggesting restaurants themselves contribute substantially to overall delivery inefficiency.

- **A large concentration of orders occurs during late evening and nocturnal hours** creating operational pressure during peak demand windows and contributing directly to increased delays.

- **ASAP orders dominate customer behavior at approximately 79.85%** confirming that most customers expect immediate fulfillment rather than scheduled delivery windows.

- **Net Revenue remains significantly lower than Gross Order Value after accounting for discounts and refunded amounts** demonstrating how operational inefficiencies directly reduce retained business value.

- **Refund rates rise alongside worsening delivery performance metrics** suggesting operational delays are likely contributing to customer dissatisfaction and compensation costs.

- **Union City generates the strongest net revenue performance among delivery areas** while Fremont contributes the lowest operational revenue output.

- **Fast preparation orders dominate the operational distribution** but delayed and slow orders still represent a meaningful operational burden affecting overall delivery consistency.

- **Order demand peaks during specific night periods while operational performance simultaneously declines** revealing a direct imbalance between customer demand intensity and operational capacity.

---

## Data Analysis

Using Power BI and DAX, the following operational measures and calculated columns were developed:

### Core Operational Measures

```dax
Total Orders = COUNTROWS('Food Delivery')

Total Customers = DISTINCTCOUNT('Food Delivery'[Customer ID])

Gross Order Value =
SUM('Food Delivery'[Sub Total]) +
SUM('Food Delivery'[Delivery fee]) +
SUM('Food Delivery'[Service fee])

Net Revenue =
SUM('Food Delivery'[Sub Total]) +
SUM('Food Delivery'[Delivery fee]) +
SUM('Food Delivery'[Service fee]) -
SUM('Food Delivery'[Discount]) -
SUM('Food Delivery'[Refunded amount])

Total Refund =
SUM('Food Delivery'[Refunded amount])

Total Discount =
SUM('Food Delivery'[Discount])

```

###  Operational Timing Measures

```dax
Avg Delivery Time = 
AVERAGE('Food Delivery'[Total Delivery Time (Minutes)])

Avg prep Time = 
ROUND( AVERAGE('Food Delivery'[Prep Time (Minutes)]), 0) & " Mins"

Avg Driver Delay = 
ROUND (AVERAGE( 'Food Delivery'[Driver Delay (Minutes)] ), 0) & " Mins"

Delayed Orders = 
CALCULATE(
    COUNTROWS('Food Delivery'),
    'Food Delivery'[Total Delivery Time (Minutes)] > 60
)

Delay Rate % = 
DIVIDE(
    [Delayed Orders],
    COUNTROWS('Food Delivery')
)

```

###  Customer Behavior Measures

```dax
 Avg Orders per Customer = 
DIVIDE(
    COUNTROWS('Food Delivery'),
    DISTINCTCOUNT('Food Delivery'[Customer ID])
)

```


###  Time Intelligence Columns
```dax
  Preparartion Category = 
SWITCH(
    TRUE(),
    'Food Delivery'[Prep Time (Minutes)] <= 30, "Fast",
    'Food Delivery'[Prep Time (Minutes)] <= 60, "Normal",
    'Food Delivery'[Prep Time (Minutes)] <= 120, "Slow",
    'Food Delivery'[Prep Time (Minutes)] > 120, "Delayed",
    BLANK()
)

```

## Results / Findings

From the complete operational analysis across all dashboards:

- Wednesday emerged as the strongest business day operationally and financially generating both the highest order volume and highest revenue while simultaneously maintaining the fastest preparation speed.
- Operational efficiency directly influences customer demand behavior as faster preparation times correlate with increased order activity and stronger revenue generation.
- The delivery pipeline is experiencing severe operational inefficiencies with only 47.43% of all orders delivered on time across the platform.
- Average end-to-end delivery duration of 2 hours 18 minutes significantly exceeds expected fulfillment standards indicating major coordination inefficiencies across restaurants and drivers.
- Driver coordination delays average 55 minutes confirming that operational slowdowns are not isolated to restaurants alone but extend across logistics execution stages.
- Most customers order during late evening and nocturnal periods creating concentrated operational pressure during high-demand windows where delivery performance deteriorates most severely.
- ASAP orders account for nearly 80% of all customer requests demonstrating that the platform operates primarily in an urgency-driven delivery environment where operational speed is critical to customer satisfaction.
- Refunds and discounts materially reduce retained business value revealing that operational inefficiencies have direct financial consequences beyond customer dissatisfaction alone.
- Preparation speed acts as a hidden revenue driver as the strongest revenue periods consistently align with lower preparation durations.
- Operational performance varies significantly across delivery areas indicating that localized optimization strategies may be required rather than platform-wide assumptions.


## Recommendations

### Based on the operational insights derived from the analysis:

- Reduce restaurant preparation time during peak demand periods through improved kitchen workflow coordination and staffing optimization.
- Increase driver allocation during late evening demand windows where operational pressure and delivery delays are highest.
- Implement proactive delay monitoring systems to identify high-risk orders before fulfillment targets are missed.
- Prioritize operational improvements around ASAP orders since urgency-based customers dominate platform demand and are most sensitive to delays.
- Investigate delivery areas with weaker operational performance separately rather than applying generalized operational assumptions across all regions.
