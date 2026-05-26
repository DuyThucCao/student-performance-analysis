# Student Academic Performance Analysis

![R](https://img.shields.io/badge/R-4.x-276DC3?style=flat&logo=r&logoColor=white)
![tidyverse](https://img.shields.io/badge/tidyverse-1.3-1A162D?style=flat)
![plotly](https://img.shields.io/badge/plotly-interactive-3F4F75?style=flat)
![Status](https://img.shields.io/badge/status-complete-brightgreen?style=flat)
![License](https://img.shields.io/badge/license-MIT-blue?style=flat)

> An end-to-end exploratory data analysis of 1,000 student records, identifying academic risk factors and performance patterns across majors, seniority levels, and GPA tiers — with interactive visualizations designed to support academic advising decisions.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Key Findings](#key-findings)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Visualizations](#visualizations)
- [Repository Structure](#repository-structure)
- [How to Run](#how-to-run)
- [Technologies](#technologies)
- [Author](#author)

---

## Project Overview

Academic institutions collect rich performance data, yet the insights buried within it often go untranslated into actionable support for students. This project bridges that gap by applying a rigorous EDA workflow to the `moody2022` dataset — cleaning raw records, engineering risk flags, and producing interactive visualizations that allow advisors and department heads to explore performance trends at a glance.

The analysis answers three core questions:
1. **Which majors and seniority groups are most at risk of academic failure?**
2. **How are GPA and test scores distributed — and do they measure the same thing?**
3. **What actionable signals can guide targeted tutoring and resource allocation?**

---

## Key Findings

| Finding | Detail |
|---|---|
| **CS has the highest mean score** | Computer Science students average the highest test scores across all majors |
| **Psychology leads in mean GPA** | Psychology students record the highest average GPA despite lower test scores in some cases |
| **Score–GPA correlation is positive but imperfect** | A clear positive relationship exists, but the two metrics capture meaningfully different dimensions of performance |
| **At-risk concentration varies by major** | The `at_risk` flag (score < 50 AND GPA < 2.0) reveals disproportionate concentration in specific major–seniority combinations |
| **GPA is relatively stable across seniority** | No dramatic grade inflation or deflation pattern is observed as students advance from Freshman to Senior year |
| **Score distributions are bimodal in some majors** | Several disciplines show a high-performer cluster and a struggling cluster with few students in between |

---

## Dataset

| Field | Description |
|---|---|
| `Major` | Student's declared major (CS, Economics, Psychology, Statistics) |
| `Score` | Numeric test score (0–100) |
| `Seniority` | Academic year (Freshman, Sophomore, Junior, Senior) |
| `GPA` | Grade Point Average (0.0–4.0) |
| `Grade` | Letter grade earned (A, B, C, D, F) |

- **Rows:** 1,000 student records
- **Source:** `moody2022.csv`
- **Completeness:** Rows with missing `score`, `gpa`, or `grade` are excluded during cleaning

---

## Methodology

### 1. Data Cleaning
- Standardized column names using `janitor::clean_names()`
- Dropped rows with missing values in key performance fields
- Converted `seniority` and `grade` to ordered factors for correct plot ordering

### 2. Feature Engineering
Two derived variables were constructed to enrich the analysis:

- **`at_risk`** — Boolean flag marking students with `score < 50` **AND** `gpa < 2.0`, identifying those who may need immediate academic intervention
- **`gpa_tier`** — Ordinal GPA band variable with four levels:
  - `Needs Improvement` (0.0–2.0)
  - `Average` (2.0–3.0)
  - `Good` (3.0–3.7)
  - `Excellent` (3.7–4.0)

### 3. Exploratory Data Analysis
- Cross-tabulations of major × seniority enrollment
- Descriptive statistics (mean, median, SD) for `score` and `gpa` by major
- At-risk student counts and rates by major and seniority
- GPA tier distribution by major
- Spearman rank correlation between `score` and `gpa`

### 4. Visualization
All plots are built with `ggplot2` and rendered interactive via `plotly`:
- Box plots: GPA and Score by Grade, GPA by Major, GPA by Seniority
- Faceted histograms: Score distributions by Major
- Grouped bar chart: Grade distribution by Major
- Scatter plot: Score vs. GPA colored by Major (full dataset)
- Heatmap: At-risk rate by Major and Seniority

---

## Visualizations

> Rendered as an interactive HTML notebook. Open `output/Student-Academic-Performance.nb.html` in any browser — no R installation required.

**Sample plots included:**

- 📦 GPA distribution by letter grade (box plot)
- 📦 Score distribution by letter grade (box plot)
- 📊 Score distributions faceted by major (histogram)
- 📦 GPA across seniority levels (box plot)
- 📊 Grade frequencies by major (grouped bar)
- 🔵 Score vs. GPA relationship by major (scatter)
- 🟥 At-risk rate heatmap by major × seniority

---

## Repository Structure

```
student-academic-performance/
├── data/
│   └── moody2022.csv              # Raw dataset (1,000 student records)
├── analysis/
│   └── Student-Academic-Performance.Rmd   # Full R Markdown analysis
├── output/
│   └── Student-Academic-Performance.nb.html  # Rendered interactive report
└── README.md
```

---

## How to Run

### Prerequisites
Install the following R packages if not already available:

```r
install.packages(c("tidyverse", "knitr", "DT", "plotly", "janitor"))
```

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/DuyThucCao/student-academic-performance.git
   cd student-academic-performance
   ```

2. **Open the R Markdown file** in RStudio:
   ```
   analysis/Student-Academic-Performance.Rmd
   ```

3. **Knit the document** using the "Knit" button or:
   ```r
   rmarkdown::render("analysis/Student-Academic-Performance.Rmd")
   ```

4. **View the interactive report** — open `output/Student-Academic-Performance.nb.html` in a browser.

> **No R needed to view results** — the pre-rendered HTML notebook in `output/` works in any modern browser.

---

## Technologies

| Tool | Purpose |
|---|---|
| **R / RStudio** | Primary analysis environment |
| **tidyverse** | Data wrangling (dplyr, readr, tidyr) and visualization (ggplot2) |
| **plotly** | Interactive chart rendering |
| **janitor** | Column name standardization and tabyl |
| **DT** | Interactive HTML data tables |
| **knitr** | Report generation and table formatting |

---

## Author

**Thuc Cao**  
B.S. Data Science, Minor in Economics & Statistics — Rutgers University (Expected May 2026)  
Data Scientist Intern — Hitachi Vantara Digital Services

[LinkedIn](https://linkedin.com/in/thucduycao) · [GitHub](https://github.com/DuyThucCao) · duythuccao@outlook.com
