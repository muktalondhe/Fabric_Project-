# ⛏️ Environmental Compliance Analytics Platform | Microsoft Fabric

## 📌 Project Overview

This project demonstrates an end-to-end **Data Engineering and Business Intelligence solution for mining operations** using **Microsoft Fabric and Power BI**.

The objective was to transform raw mining operational data into a **secure, scalable, and analytics-ready platform** for environmental compliance monitoring, operational analysis, and business decision-making.

The project handles datasets with different levels of granularity, including:

* Daily methane emission records
* High-frequency machinery telemetry
* Production data
* Fuel and operational cost data
* Regional and site information

To manage these datasets efficiently, the solution implements a **Medallion Architecture (Bronze, Silver, Gold)** and a **Galaxy Schema Semantic Model** in Microsoft Fabric.

---

## 🏗️ Architecture

```text
                    ┌─────────────────────────┐
                    │      Raw Data Sources   │
                    │                         │
                    │ • Methane Data          │
                    │ • Machinery Telemetry   │
                    │ • Production Data       │
                    │ • Fuel / Cost Data      │
                    └────────────┬────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │     Microsoft Fabric    │
                    │        OneLake           │
                    └────────────┬────────────┘
                                 │
                                 ▼
              ┌──────────────────────────────────┐
              │          🥉 Bronze Layer          │
              │                                  │
              │ Raw / Ingested Data              │
              └────────────────┬─────────────────┘
                               │
                               ▼
              ┌──────────────────────────────────┐
              │          🥈 Silver Layer          │
              │                                  │
              │ Data Cleaning                    │
              │ Standardization                  │
              │ Transformation                   │
              │ Data Preparation                 │
              └────────────────┬─────────────────┘
                               │
                               ▼
              ┌──────────────────────────────────┐
              │           🥇 Gold Layer           │
              │                                  │
              │ Business-Ready Fact Tables       │
              │ Dimension Tables                 │
              │ Aggregated / Analytical Data     │
              └────────────────┬─────────────────┘
                               │
                               ▼
              ┌──────────────────────────────────┐
              │      Galaxy Schema Model         │
              │                                  │
              │ Multiple Fact Tables             │
              │ Shared Dimensions                │
              └────────────────┬─────────────────┘
                               │
                               ▼
              ┌──────────────────────────────────┐
              │       Power BI Semantic Model    │
              │                                  │
              │ DAX Measures + RLS               │
              └────────────────┬─────────────────┘
                               │
                               ▼
                    ┌───────────────────────┐
                    │   Power BI Dashboard  │
                    │                       │
                    │ Executive Overview    │
                    │ Regional Analysis      │
                    │ Methane Analysis      │
                    │ Machinery Analytics   │
                    │ Compliance Dashboard  │
                    └───────────────────────┘
```

---

## 🛠️ Technologies Used

| Technology                   | Purpose                            |
| ---------------------------- | ---------------------------------- |
| **Microsoft Fabric**         | End-to-end data platform           |
| **OneLake**                  | Centralized data storage           |
| **Fabric Lakehouse**         | Data storage and processing        |
| **Dataflow Gen2**            | Data cleansing and transformation  |
| **Power BI**                 | Data visualization and reporting   |
| **DAX**                      | Business calculations and KPIs     |
| **Semantic Model**           | Analytical data modeling           |
| **Galaxy Schema**            | Multiple fact table modeling       |
| **Medallion Architecture**   | Bronze-Silver-Gold data processing |
| **Row-Level Security (RLS)** | Role-based data access             |

---

# 🔄 Data Engineering Workflow

## 1. 🥉 Bronze Layer — Raw Data Ingestion

Raw mining datasets were ingested into **Microsoft Fabric OneLake** and organized within the Bronze Layer.

The Bronze Layer preserves the source-level data before applying major transformations.

### Key activities

* Data ingestion
* Source data organization
* Raw data storage
* Initial validation
* Maintaining source-level structure

---

## 2. 🥈 Silver Layer — Data Transformation

The Silver Layer was created using **Dataflow Gen2** to clean, standardize, and prepare the data for analytics.

### Transformations included

* Handling missing values
* Data type standardization
* Column standardization
* Data cleansing
* Removing inconsistencies
* Preparing analytical datasets
* Standardizing dates and operational attributes

The goal was to create reliable and consistent datasets for the Gold Layer.

---

## 3. 🥇 Gold Layer — Business-Ready Data

The Gold Layer contains business-ready tables designed specifically for reporting and analytics.

The model includes multiple fact tables representing different business processes along with shared dimensions.

### Example Fact Tables

* `FactMethane`
* `FactMachinery`
* `FactProduction`
* `FactOperations`

### Example Dimensions

* `DimDate`
* `DimTime`
* `DimLocation`
* `DimRegion`
* `DimMachinery`

> The exact table names can be adjusted according to the final Fabric implementation.

---

# ⭐ Galaxy Schema Semantic Model

Because the project contains multiple business processes with different granularities, a traditional single-star schema would not be sufficient.

A **Galaxy Schema** was implemented to support multiple fact tables that share common dimensions.

```text
                    DimDate
                       │
                       │
          ┌────────────┼────────────┐
          │            │            │
          ▼            ▼            ▼
    FactMethane   FactProduction  FactMachinery
          │            │            │
          │            │            │
          └───────┬────┴────────────┘
                  │
             Shared Dimensions
                  │
          ┌───────┴────────┐
          ▼                ▼
     DimLocation       DimRegion
```

### Benefits

* Handles multiple business processes
* Supports different data granularities
* Reduces unnecessary duplication
* Improves analytical flexibility
* Enables consistent filtering across fact tables
* Supports scalable Power BI reporting

---

# 📊 Power BI Dashboard

The final solution contains a **5-page interactive Power BI dashboard**.

## 1. Executive Overview

Provides a high-level view of mining operations and environmental performance.

### Key metrics

* Total Production
* Total Emissions
* Methane Emissions
* Operational Costs
* Fuel Consumption
* Compliance KPIs

---

## 2. Regional Analysis

Provides regional and site-level performance analysis.

### Analysis includes

* Production by region
* Emissions by region
* Operational performance
* Regional comparison
* Site-level performance

---

## 3. Methane Leak Analysis

Focuses on methane monitoring and environmental compliance.

### Analysis includes

* Methane emissions
* Leak trends
* Emission intensity
* Location-wise methane levels
* Time-based emission analysis
* Compliance monitoring

---

## 4. Machinery & Fuel Analytics

Provides insights into machinery operations and fuel usage.

### Analysis includes

* Machinery utilization
* Fuel consumption
* Operational activity
* Machinery-level performance
* Cost analysis
* Efficiency indicators

---

## 5. Compliance Dashboard

Provides a consolidated view of environmental compliance.

### Analysis includes

* Compliance status
* Emission thresholds
* Methane monitoring
* Regional compliance
* Environmental KPIs
* Exception identification

---

# 🧮 DAX Measures

Several DAX measures were created to support business analysis.

Examples include:

```DAX
Total Production =
SUM(FactProduction[Production])
```

```DAX
Total Methane Emissions =
SUM(FactMethane[Methane_Emission])
```

```DAX
Total Operational Cost =
SUM(FactOperations[Operational_Cost])
```

```DAX
Total Fuel Consumption =
SUM(FactMachinery[Fuel_Consumption])
```

Additional measures were created for:

* Production analysis
* Emission tracking
* Methane monitoring
* Operational costs
* Compliance analysis
* Year-over-Year analysis
* KPI calculations

---

# 🔐 Security & Governance

Security was implemented to provide different levels of access for different user personas.

### 👔 Leadership

Leadership users receive access to:

* Executive KPIs
* Regional performance
* Production analysis
* Environmental performance
* Overall compliance information

### 🕵️ Inspector

Inspector users receive access focused on:

* Environmental monitoring
* Methane analysis
* Compliance information
* Operational inspection data

### Security Features

* Role-Based Access
* Row-Level Security (RLS)
* Governed semantic model
* Controlled report access
* Secure Fabric workspace

---

# 🚀 Key Features

✅ Microsoft Fabric Workspace setup

✅ OneLake-based data storage

✅ Fabric Lakehouse implementation

✅ Medallion Architecture

✅ Bronze → Silver → Gold data pipeline

✅ Dataflow Gen2 transformations

✅ Multiple fact tables

✅ Galaxy Schema data model

✅ Shared dimensions

✅ Power BI Semantic Model

✅ DAX measures

✅ Interactive Power BI dashboard

✅ Environmental compliance monitoring

✅ Methane emission analysis

✅ Machinery and fuel analytics

✅ Role-Based Security

✅ Secure and governed reporting

---

# 💡 Key Challenges & Solutions

## Challenge 1 — Different Data Granularities

The project contained daily methane data and high-frequency machinery telemetry.

### Solution

A Galaxy Schema was designed with separate fact tables while using shared dimensions wherever appropriate.

---

## Challenge 2 — Raw and Inconsistent Data

Raw datasets required cleaning and standardization before analytics.

### Solution

Dataflow Gen2 was used in the Silver Layer to perform cleansing, transformation, and standardization.

---

## Challenge 3 — Multiple Business Requirements

Different stakeholders required different analytical views.

### Solution

A Power BI semantic model with reusable DAX measures was created to support multiple dashboard pages and business requirements.

---

## Challenge 4 — Data Security

Leadership and inspectors required different levels of access.

### Solution

Role-Based Security and Row-Level Security were implemented to control access to relevant information.

---

# 📈 Business Value

The solution provides a centralized analytics platform that can help mining organizations:

* Monitor environmental performance
* Track methane emissions
* Identify potential compliance issues
* Analyze machinery efficiency
* Monitor fuel consumption
* Compare regional performance
* Track operational costs
* Support data-driven decision-making
* Improve governance and controlled data access

---

# 🧠 Key Learnings

This project strengthened my practical understanding of:

* Microsoft Fabric
* OneLake
* Lakehouse Architecture
* Medallion Architecture
* Data Engineering
* Data Transformation
* Data Modeling
* Galaxy Schema
* Semantic Models
* Power BI
* DAX
* Row-Level Security
* Data Governance
* Environmental Compliance Analytics

---

# 📂 Project Structure

```text
Environmental-Compliance-Fabric/
│
├── README.md
│
├── Data/
│   ├── Raw/
│   ├── Bronze/
│   ├── Silver/
│   └── Gold/
│
├── Fabric/
│   ├── Workspace/
│   ├── Lakehouse/
│   ├── Dataflows/
│   └── Semantic_Model/
│
├── PowerBI/
│   ├── Executive_Overview/
│   ├── Regional_Analysis/
│   ├── Methane_Analysis/
│   ├── Machinery_Fuel/
│   └── Compliance/
│
├── Documentation/
│   ├── Architecture/
│   ├── Data_Model/
│   └── Security/
│
└── Screenshots/
    ├── Architecture.png
    ├── Data_Model.png
    ├── Executive_Overview.png
    ├── Regional_Analysis.png
    ├── Methane_Analysis.png
    ├── Machinery_Fuel.png
    └── Compliance.png
```

---

# 📸 Dashboard Preview

### Executive Overview

*Add your Executive Overview screenshot here.*

### Regional Analysis

*Add your Regional Analysis screenshot here.*

### Methane Leak Analysis

*Add your Methane Analysis screenshot here.*

### Machinery & Fuel Analytics

*Add your Machinery & Fuel screenshot here.*

### Compliance Dashboard

*Add your Compliance Dashboard screenshot here.*

---

# 🔮 Future Enhancements

Potential improvements for the platform include:

* Real-time machinery telemetry ingestion
* Automated data quality monitoring
* Fabric Data Pipelines for orchestration
* Incremental data processing
* Automated compliance alerts
* Machine learning-based methane anomaly detection
* Predictive machinery maintenance
* Microsoft Fabric Real-Time Intelligence
* Automated reporting and notifications

---

# 👩‍💻 Author

**Mukta Londhe**

Data Engineer | Data Analyst

**Skills:**
Python • SQL • Microsoft Fabric • Databricks • Power BI • DAX • ETL • Data Modeling • Lakehouse • Data Analytics

---

## ⭐ Project Highlights

> **Raw Mining Data → Fabric Lakehouse → Medallion Architecture → Galaxy Schema → Semantic Model → Power BI → Secure Environmental Compliance Analytics**

This project demonstrates how modern data engineering practices can be combined with business intelligence to build a scalable and governed analytics solution.
