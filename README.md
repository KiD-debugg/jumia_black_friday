# Jumia Black Friday 2026 Product Analysis

## Overview

This project analyzes a snapshot of Jumia product listings collected for the 2026 Black Friday campaign. It uses Python, pandas, and data visualization libraries to examine product categories, prices, discounts, ratings, seller types, promotional activity, and listing-position behavior.

The analysis is presented through a Jupyter notebook and is designed for an exploratory, descriptive study of the marketplace. The dataset contains **7,986 unique product listings** and was scraped on **3 November 2026**.

> This project describes the supplied dataset only. It does not establish that observed relationships are causal, and it does not represent Jumia's complete catalogue or all of a campaign period.

## Business Objectives

The project answers practical questions relevant to customers, sellers, and marketplace analysts:

- Which product categories have the largest number of listings?
- What proportion of listings come from official stores?
- How large are Black Friday discounts, and how do they vary by category?
- How are current prices distributed?
- What is the relationship between advertised discounts and customer ratings?
- How do ratings differ between official and non-official stores?
- How does promotional positioning change across listing pages?
- How do original prices compare with current prices?

## Dataset

**Source file:** `data/raw/jumia_black_friday_2026.csv`

**Notebook:** `notebooks/analysis.ipynb`

| Property | Value |
|---|---:|
| Records | 7,986 |
| Columns | 24 |
| Unique product IDs | 7,986 |
| Scrape date | 3 November 2026 |
| Product categories | 16 |
| Brands | 615 |
| Listing sources | 14 |

### Key Fields

| Field group | Examples |
|---|---|
| Product identity | `product_id`, `product_name`, `brand` |
| Classification | `category`, `sub_category`, `product_type`, `product_subtype` |
| Pricing | `current_price_ksh`, `original_price_ksh`, `discount_pct`, `discount_amount_ksh`, `price_band` |
| Customer feedback | `rating`, `review_count`, `has_rating`, `rating_band` |
| Seller and listing attributes | `is_official_store`, `listing_source`, `listing_page`, `listing_position` |
| Promotions | `has_price_variants`, `num_promo_tags`, `discount_band` |

## Data Quality Summary

The dataset has no duplicate product IDs and no missing values in core commercial fields such as product ID, price, discount, review count, and listing metadata.

| Field | Missing records |
|---|---:|
| `sub_category` | 130 |
| `product_type` | 232 |
| `product_subtype` | 1,666 |
| `rating` | 2,709 |

The 2,709 missing ratings correspond to 33.92% of listings and should not be interpreted as low ratings. The notebook distinguishes rated and unrated items through `has_rating` and `rating_band`.

## Key Findings

The following figures are descriptive statistics from the supplied dataset:

- **Official-store share:** 10.14% of listings (810 of 7,986).
- **Rated listings:** 66.08% of listings (5,277 of 7,986).
- **Average discount:** 43.83%.
- **Median discount:** 46%.
- **Median current price:** KSh 949.
- **Average current price:** KSh 2,359.85.

### Category Distribution

The largest product categories by listing count are:

| Rank | Category | Listings |
|---:|---|---:|
| 1 | Fashion | 748 |
| 2 | Phones & Tablets | 632 |
| 3 | Home & Office | 613 |
| 4 | Electronics | 609 |
| 5 | Computing | 606 |
| 6 | Health & Beauty | 604 |
| 7 | Grocery | 601 |
| 8 | Baby Products | 600 |
| 9 | Automobile | 600 |
| 10 | Sporting Goods | 600 |

### Discount Insights

- Fashion has the highest average listed discount among categories with meaningful volume at approximately **51.15%**.
- Toys & Games follows at approximately **49.23%**.
- Phones & Tablets and Computing also have average discounts above **46%**.
- These averages compare categories with very different products and price ranges, so they are most useful as descriptive segment insights rather than direct price-quality comparisons.

### Rating and Store Insights

Among rated products:

- The average rating for non-official-store listings is approximately **4.01**.
- The average rating for official-store listings is approximately **4.27**.
- Approximately 66% of listings have a recorded rating.

The Pearson correlation between discount percentage and rating is approximately **-0.085**. This weak negative relationship provides no evidence that larger discounts reliably lead to better or worse ratings.

Current price and original price have a strong positive correlation of approximately **0.955**, while differences may still contain a mix of genuine markdowns and promotional price presentation.

## Analysis Conducted

The notebook combines basic data profiling with univariate, bivariate, categorical, and visual analysis.

### Data Preparation and Validation

- Loads the CSV using pandas.
- Reviews column names, sample records, dimensions, data types, and unique values.
- Checks missing values and duplicate product IDs.
- Uses 0/1 flags and derived bands for categorical analysis.
- Retains missing ratings and unrated listings explicitly rather than silently imputing them.

### Descriptive Visualizations

- **Bar charts:** product counts by category and rating band.
- **Horizontal bar charts:** brands with the most product listings.
- **Grouped bar charts:** rating, discount, and price-segment composition.
- **Histograms:** discount, price, and rating distributions.
- **Box plots:** category-level variation in discounts and potential outliers.
- **Scatter plots:** discount versus rating, original versus current price, and review count versus promotion count.
- **Line charts:** average discount and price across listing pages.
- **Pie and donut charts:** official-versus-non-official-store share.

## Technology Stack

| Component | Technology |
|---|---|
| Language | Python 3.14.4 |
| Data manipulation | pandas 3.1.1 |
| Numerical computing | NumPy 2.5.4 |
| Core visualization | Matplotlib 3.11.2 |
| Statistical visualization | seaborn 0.13.2 |
| Interactive environment | Jupyter Notebook / VS Code |

Package versions are recorded from the local project virtual environment. They can be confirmed by running:

```powershell
& .\Scripts\python.exe -c "import pandas, numpy, matplotlib, seaborn; print(pandas.__version__, numpy.__version__, matplotlib.__version__, seaborn.__version__)"
```

## Project Structure

```text
jumia_black_friday/
|-- README.md
|-- pyvenv.cfg
|-- Scripts/
|-- Lib/
|-- notebooks/
|   `-- analysis.ipynb
`-- data/
    `-- raw/
        `-- jumia_black_friday_2026.csv
```

Virtual-environment folders such as `Scripts/` and `Lib/` should generally not be committed to source control. Consider adding them to `.gitignore` and reproducing the environment from a dependency manifest.

## Setup Instructions

### 1. Clone or Open the Project

```powershell
cd F:\projects1\jumia_black_friday
```

### 2. Activate the Virtual Environment

Command Prompt:

```bat
Scripts\activate.bat
```

PowerShell:

```powershell
& .\Scripts\Activate.ps1
```

If the environment cannot be activated due to a PowerShell execution-policy restriction, use Command Prompt or run VS Code from the activated environment.

### 3. Confirm the Kernel

Use the notebook kernel:

```text
F:\projects1\jumia_black_friday\Scripts\python.exe
```

### 4. Launch Jupyter

```powershell
python -m pip install jupyter
jupyter notebook
```

Then open `notebooks/analysis.ipynb`.

## Reproduce the Analysis

From the project root:

```powershell
& .\Scripts\python.exe -m jupyter notebook notebooks\analysis.ipynb
```

Run all notebook cells in order. The notebook currently contains a Windows-specific absolute CSV path. To make the project portable, replace it with a path based on the notebook working directory or relative project path.

Example:

```python
from pathlib import Path

project_root = Path.cwd().parent
jumia_data = pd.read_csv(project_root / "data" / "raw" / "jumia_black_friday_2026.csv")
```

## Interpretation and Limitations

- The snapshot is not necessarily representative of Jumia's complete catalogue.
- One category, brand, or product group may be overrepresented by the collection method.
- The scrape date may cover a static moment rather than the entire campaign.
- Missing ratings are meaningful and should not be removed without documenting the effect.
- Outliers and extreme prices can materially affect means.
- Correlations measure association, not causation.
- Product discounts may reflect the original and current values supplied in the listing and require verification against historical prices.
- Listing-page and position metrics describe placement at collection time, not long-term campaign performance.
- Discount and rating relationships may be affected by listing quality, brand, category, seller reputation, and product lifecycle.

## Recommended Next Steps

1. Add automated data validation for schema, ranges, duplicate IDs, and impossible price relationships.
2. Replace the absolute file path with portable project-relative paths.
3. Export figures to `reports/figures/` for presentations and stakeholder reports.
4. Add a written executive summary of the campaign findings.
5. Separate exploratory data analysis from reusable data-cleaning functions.
6. Create a compact `requirements.txt` or `pyproject.toml`.
7. Investigate category-adjusted rating and discount patterns.
8. Compare the same product across brands and pages while controlling for rating availability.
9. Track the same products across multiple scrape dates to assess real campaign changes.
10. Add tests for cleaned fields, including discount consistency:
    `discount_amount_ksh = original_price_ksh - current_price_ksh`.

## Reusability

The notebook's structure can be reused for other retail listing datasets if the CSV contains compatible columns for price, category, brand, rating, seller status, promotion tags, and listing position.
