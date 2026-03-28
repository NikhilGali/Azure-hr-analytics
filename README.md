# Azure HR Analytics Pipeline & Workforce Insights Dashboard

> **Enterprise-grade HR data pipeline built on Azure Data Factory + Power BI** — ingesting employee, payroll, attendance, and performance datasets into Azure Synapse Analytics, with a Star Schema data model and an interactive Power BI workforce dashboard.

---

## 📌 Project Overview

| Item | Detail |
|------|--------|
| **Timeline** | Jan 2026 – Feb 2026 |
| **Domain** | Human Resources / Workforce Analytics |
| **Stack** | Azure Data Factory · Azure Synapse Analytics · Azure SQL · Power BI · Python · SQL |
| **Records Processed** | 50,000+ HR records |
| **Key Outcome** | 70% reduction in manual HR reporting effort |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                        DATA SOURCES (Raw)                           │
│  employee_master.csv │ payroll.csv │ attendance.csv │ performance.csv│
└───────────────┬─────────────────────────────────────────────────────┘
                │
                ▼
┌─────────────────────────────┐
│   Azure Data Factory (ADF)  │  ← Linked Services, Parameterized
│   Pipelines + Triggers      │    Datasets, Incremental Loads
└───────────────┬─────────────┘
                │
                ▼
┌──────────────────────────────────────────┐
│  Azure Synapse Analytics / Azure SQL     │
│  Star Schema: fact_employee              │
│               dim_department             │
│               dim_date                   │
│               dim_job_role               │
└───────────────┬──────────────────────────┘
                │
                ▼
┌─────────────────────────────┐
│  Power BI Dashboard         │  ← DAX KPIs, RLS, Scheduled Refresh
│  Workforce Insights         │
└─────────────────────────────┘
```

---

## 📁 Repository Structure

```
azure-hr-analytics/
│
├── data/
│   ├── raw/                        # Sample source CSVs (anonymized)
│   │   ├── employee_master.csv
│   │   ├── payroll.csv
│   │   ├── attendance.csv
│   │   └── performance.csv
│   └── processed/                  # Post-pipeline clean data
│       └── fact_employee_sample.csv
│
├── notebooks/
│   ├── 01_data_generation.ipynb    # Generate synthetic HR data
│   ├── 02_eda_hr_analysis.ipynb    # Exploratory Data Analysis
│   └── 03_attrition_analysis.ipynb # Attrition risk modeling
│
├── sql/
│   ├── 01_create_schema.sql        # Star schema DDL
│   ├── 02_load_dimensions.sql      # Dimension table loads
│   ├── 03_load_fact_employee.sql   # Fact table load
│   └── 04_kpi_queries.sql          # KPI validation queries
│
├── adf_pipelines/
│   ├── pipeline_employee_ingest.json
│   ├── pipeline_payroll_ingest.json
│   └── pipeline_master_orchestrator.json
│
├── powerbi/
│   └── HR_Analytics_Dashboard.md   # Dashboard layout & DAX measures
│
├── docs/
│   └── architecture_diagram.md
│
├── requirements.txt
└── README.md
```

---

## 🔧 Tech Stack

- **Azure Data Factory (ADF)** — Linked services, copy activities, parameterized pipelines, schedule triggers
- **Azure Synapse Analytics / Azure SQL** — Data warehouse, Star Schema modeling
- **Power BI** — DAX measures, Row-Level Security (RLS), scheduled dataset refresh
- **Python** — Data generation, EDA, attrition analysis (pandas, numpy, matplotlib, seaborn, scikit-learn)
- **SQL (T-SQL)** — Schema creation, transformation, KPI queries

---

## 🚀 Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/YOUR_USERNAME/azure-hr-analytics.git
cd azure-hr-analytics
```

### 2. Install Python Dependencies
```bash
pip install -r requirements.txt
```

### 3. Generate Synthetic HR Data
```bash
jupyter notebook notebooks/01_data_generation.ipynb
```

### 4. Set Up Azure SQL Schema
Run the SQL scripts in order against your Azure SQL / Synapse instance:
```bash
# Connect to your Azure SQL and run:
01_create_schema.sql
02_load_dimensions.sql
03_load_fact_employee.sql
```

### 5. Deploy ADF Pipelines
- Import the JSON files in `adf_pipelines/` into your Azure Data Factory instance
- Configure linked services with your Azure SQL connection string
- Set trigger schedules as needed

### 6. Connect Power BI
- Open Power BI Desktop → Get Data → Azure SQL Database
- Use the DAX measures documented in `powerbi/HR_Analytics_Dashboard.md`
- Configure RLS roles per department

---

## 📊 Power BI Dashboard — KPIs

| KPI | DAX Measure |
|-----|-------------|
| Attrition Rate | `DIVIDE([Employees Left], [Total Employees])` |
| Headcount MoM Change | `[Current Headcount] - [Prior Month Headcount]` |
| Avg Absenteeism Rate | `DIVIDE([Total Absent Days], [Total Working Days])` |
| Avg Performance Score | `AVERAGE(fact_employee[performance_score])` |
| Payroll Cost per Employee | `DIVIDE([Total Payroll], [Total Employees])` |

---

## 📈 Key Results

- ✅ **50,000+ HR records** processed through ADF incremental pipelines
- ✅ **70% reduction** in manual HR reporting time
- ✅ **10+ KPIs** tracked in real-time via Power BI
- ✅ **Row-Level Security** enforced — managers see only their department data
- ✅ Zero data reconciliation errors post-automation

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

## 👤 Author

**Nikhil Sai Gali**  
MS Information Science — University at Albany, NY  
[LinkedIn](https://linkedin.com/in/YOUR_PROFILE) · [GitHub](https://github.com/YOUR_USERNAME)
