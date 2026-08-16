# Product-Sales-Analysis-Project
# 📊 Product Sales Analysis — Amazon Electronics

Exploratory data analysis of Amazon's electronics category, uncovering trends in customer ratings, brand performance, and category demand across two decades of sales activity — delivered through Python/Jupyter notebooks and an interactive Power BI dashboard.

![Python](https://img.shields.io/badge/Python-3.9-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Wrangling-150458?logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-4C72B0)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

---

## Table of Contents

- [Overview](#overview)
- [Key Insights](#key-insights)
- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Methodology](#methodology)
- [Power BI Dashboard](#power-bi-dashboard)
- [Sample Analysis Questions Answered](#sample-analysis-questions-answered)
- [Notes on Repository Size](#notes-on-repository-size)
- [Future Improvements](#future-improvements)
- [License](#license)
- [Acknowledgments](#acknowledgments)

---

## Overview

This project analyzes over **1.29 million** Amazon electronics reviews/ratings spanning **1999–2018** to answer practical business questions such as:

- Which years and months drive the most sales activity?
- Which brands and product categories perform best (and worst)?
- How are customer ratings distributed, and what does that say about satisfaction?
- How do top-performing brands shift year over year?

The analysis is performed twice, using two complementary approaches, so the findings can be cross-validated:

1. **`Sales_Analysis.ipynb`** — uses `seaborn.countplot` for quick categorical distribution plots.
2. **`Product_Sales_Analysis.ipynb`** — uses `pandas.groupby()` aggregations paired with bar and pie charts for a more granular, count-based breakdown.

Findings from both notebooks are then consolidated into an interactive **Power BI** dashboard (`DASHBOARDS.pbix`) for stakeholder-friendly exploration.

---

## Key Insights

| Question | Finding |
|---|---|
| 🏆 Best year for sales | **2015** |
| 📅 Best month for sales | **January** |
| 🥇 Top-performing brands | **Bose** and **Logitech**, with **Mpow** and **TaoTronics** frequently placing 3rd depending on the year |
| 📉 Weakest-performing brands | **EINCAR**, **DURAGADGET**, and **Koolertron** consistently ranked lowest |
| 🎧 Best-selling category | **Headphones**, followed by **Computers & Accessories** and **Camera & Photo** |
| 🔒 Weakest category | **Security & Surveillance** |
| ⭐ Rating sentiment | Ratings are heavily skewed positive — **~58%** of all ratings are 5-star, with a mean rating around **4.0–4.2** |

> These conclusions are derived directly from the notebooks' EDA output and are reproducible by re-running the analysis (see [Getting Started](#getting-started)).

---

## Dataset

**Source:** [Amazon Electronics Dataset on Kaggle](https://www.kaggle.com/datasets/edusanketdk/electronics) *(free Kaggle account required to download)*

| Metric | Value |
|---|---|
| Total records | 1,292,954 rows |
| Unique products (`item_id`) | 9,560 |
| Unique users (`user_id`) | 1,157,633 |
| Categories | 10 |
| Time span | 1999 – 2018 |

**Schema:**

| Column | Description |
|---|---|
| `item_id` | Unique identifier for the product |
| `user_id` | Unique identifier for the reviewing user |
| `rating` | Star rating given by the user (1.0 – 5.0) |
| `timestamp` | Date the review/rating was submitted |
| `model_attr` | Demographic attribute associated with the review (`Female`, `Male`, `Female&Male`) |
| `category` | Product category (e.g., Headphones, Home Audio, Wearable Technology) |
| `brand` | Product brand (contains missing values for ~74% of records) |
| `year` | Year extracted from `timestamp` |
| `user_attr` | Additional user-level attribute (mostly missing) |
| `split` | Dataset partition flag (train/validation/test-style split) |
| `month` *(cleaned file only)* | Month extracted from `timestamp`, engineered during preprocessing |

**Product categories covered:** Portable Audio & Video, Computers & Accessories, Headphones, Camera & Photo, Television & Video, Home Audio, Accessories & Supplies, Car Electronics & GPS, Security & Surveillance, Wearable Technology.

---

## Project Structure

```
Product-Sales-Analysis/
├── README.md
└── Product_Analysis/
    ├── Sales_Analysis.ipynb                          # EDA using seaborn countplots
    ├── Product_Sales_Analysis.ipynb                   # EDA using groupby + bar/pie charts
    ├── electronics.csv                                # Raw dataset
    ├── electronics_cleaned.csv                        # Cleaned dataset (adds `month`, nulls handled)
    ├── DASHBOARDS.pbix                                # Power BI interactive dashboard
    └── Amazon_Electronics_Products_Sales/
        └── electronics.csv                            # Original Kaggle export (source copy)
```

---

## Tech Stack

- **Language:** Python 3.9
- **Data manipulation:** [pandas](https://pandas.pydata.org/), [NumPy](https://numpy.org/)
- **Visualization:** [Matplotlib](https://matplotlib.org/), [Seaborn](https://seaborn.pydata.org/)
- **Notebook environment:** Jupyter Notebook
- **Business intelligence / dashboarding:** Microsoft Power BI

---

## Getting Started

### Prerequisites

- Python 3.9+
- Jupyter Notebook or JupyterLab
- (Optional) Microsoft Power BI Desktop to open `DASHBOARDS.pbix`

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/SumitKilaniya/Product-Sales-Analysis.git
   cd Product-Sales-Analysis/Product_Analysis
   ```

2. **Create a virtual environment (recommended)**
   ```bash
   python -m venv venv
   source venv/bin/activate      # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```

4. **Launch Jupyter**
   ```bash
   jupyter notebook
   ```

5. Open either `Sales_Analysis.ipynb` or `Product_Sales_Analysis.ipynb` and run all cells sequentially.

### Running the Power BI Dashboard

Open `DASHBOARDS.pbix` in [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (Windows only). No additional configuration is required — the data model is embedded in the file.

---

## Methodology

1. **Data loading** — Import the raw CSV (`electronics.csv`) with pandas.
2. **Type correction** — Cast `user_id` and `item_id` to strings, `brand`/`category` to string type, `rating` to float, and `timestamp` to datetime.
3. **Feature engineering** — Derive `year` and `month` from `timestamp` for time-based trend analysis.
4. **Data cleaning** — Identify and handle missing values (primarily in `brand` and `user_attr`) and check for duplicate records.
5. **Descriptive statistics** — Use `.describe()` and `.nunique()` to understand distribution shape and cardinality.
6. **Exploratory visualization** — Generate count plots, grouped bar charts, and pie charts to explore:
   - Rating distribution
   - Sales volume by year and month
   - Top/bottom performing brands (overall and by year)
   - Top/bottom performing categories
7. **Synthesis** — Summarize findings into actionable conclusions (see [Key Insights](#key-insights)).

---

## Power BI Dashboard

`DASHBOARDS.pbix` translates the notebook findings into an interactive, filterable dashboard intended for non-technical stakeholders. It enables drill-down exploration of:

- Sales volume trends over time
- Brand and category leaderboards
- Rating distribution and sentiment breakdown

> Open the file in Power BI Desktop to interact with slicers and filters directly.

---

## Sample Analysis Questions Answered

- What was the best year and month for sales?
- Which brands sold the most/least overall, and how did that change year over year (2015–2018)?
- Which product categories are the strongest and weakest performers?
- What does the overall customer sentiment (rating distribution) look like?
- What were the top-selling categories specifically in January (the peak sales month)?

---

## Notes on Repository Size

This repository contains large CSV files (~80–86 MB each) and a Power BI file (~12 MB). If you're forking or cloning this project for portfolio purposes, consider:

- Using [Git LFS](https://git-lfs.github.com/) for large binary/data files, or
- Excluding raw CSVs via `.gitignore` and documenting the Kaggle download link instead (as done in this README).

`electronics.csv` appears twice in this repository (once at the `Product_Analysis` root and once inside `Amazon_Electronics_Products_Sales/`) — these are identical copies of the original Kaggle export and can be deduplicated.

---

## Future Improvements

- [ ] Deduplicate the redundant `electronics.csv` copy
- [ ] Add a `requirements.txt` / `environment.yml` for reproducible environments
- [ ] Impute or explicitly document handling of missing `brand` and `user_attr` values rather than dropping them
- [ ] Extend analysis with time-series forecasting (e.g., predicting next year's top category)
- [ ] Add cohort/user-level analysis using `user_attr` and `model_attr`
- [ ] Export static chart images into a `visuals/` folder for easier README embedding
- [ ] Add a license file

---

## License

No license file is currently included in this repository. Until one is added, all rights are reserved by the author. Consider adding an [MIT](https://choosealicense.com/licenses/mit/) or similar open-source license if you'd like others to reuse this work.

---

## Acknowledgments

- Dataset provided by [edusanketdk on Kaggle](https://www.kaggle.com/datasets/edusanketdk/electronics)
- Built with the Python data science stack: pandas, NumPy, Matplotlib, and Seaborn

---

**Author:** Sumit Kilaniya
