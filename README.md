# Exploring Customer Sales

### Your first data science project, from raw transactions to explainable findings.

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/codingmermaid/exploring-customer-sales/blob/main/exploringSales.ipynb)

A guided, beginner-friendly exploratory data analysis of **541,909 real invoice lines** from a UK online retailer. Learn to inspect messy data, make explicit cleaning decisions, visualize sales activity, and explain what your results do—and do not—support.

**By [Coding Mermaid](https://github.com/codingmermaid)** · Python · Pandas · Matplotlib · Jupyter / Google Colab

[Explore the notebook](exploringSales.ipynb) · [Start in Colab](https://colab.research.google.com/github/codingmermaid/exploring-customer-sales/blob/main/exploringSales.ipynb) · [Original dataset](https://archive.ics.uci.edu/dataset/352/online+retail)

## What you will learn

- Load an Excel dataset into a Pandas DataFrame.
- Inspect types, missing values, repeated records, and unusual quantities.
- Define analysis rules before calculating business measures.
- Use filtering, `groupby()`, aggregation, and date operations.
- Build five charts and write findings with appropriate limitations.

**Prerequisites:** basic Python variables, comparisons, and functions. Allow roughly **2–3 hours** at your own pace. This project needs no GPU and does not require machine learning experience.

## Start in Google Colab

1. Click **Open in Colab** above.
2. Save a copy to your Drive if you want to keep your edits.
3. Use a standard CPU runtime and run cells from top to bottom.
4. Read the explanations and complete at least one independent exercise.

The notebook downloads the original UCI archive automatically. You do not need to mount your Drive. If the download fails, download the archive from the [dataset page](https://archive.ics.uci.edu/dataset/352/online+retail), extract `Online Retail.xlsx`, and upload the workbook into Colab's working directory before rerunning the loading cell.

If your runtime specifically reports a missing Excel dependency, run `%pip install openpyxl` in a new code cell. When a runtime resets, rerun the earlier cells to recreate your variables.

## Questions we explore

| Question | Approach |
|---|---|
| Which products lead by recorded positive units? | Group invoice lines by product code and compare quantities |
| Which products contribute the most positive-sales value? | Aggregate quantity × unit price |
| How does sales activity change over time? | Compare complete months from January–November 2011 |
| Which customer countries account for the most value? | Report the UK share and compare other countries |
| What changes when cancellations are included? | Compare positive-sales value with signed recorded value |

## A look at the analysis

![Monthly positive-sales value from January through November 2011](images/monthly-sales.png)

*November has the highest positive-sales value in the selected window. December 2011 is excluded because the source ends on December 9. The chart describes recorded activity; it does not establish why it changed.*

## Selected findings

These figures use the notebook's filtering and deduplication policy, rather than all source records indiscriminately.

| Measure | Result |
|---|---:|
| Retained positive-sales invoice lines | 522,504 |
| Positive-sales value | £10,246,820.87 |
| Signed recorded value, including eligible cancellations | £9,770,919.71 |
| Difference between the two measures | £475,901.16 |
| UK share of positive-sales value | 85.1% |
| Highest complete month in January–November 2011 | November: £1,452,112.69 |

> **A ranking needs context.** Product `23843` leads the positive-unit ranking with 80,995 units, but the source also records an equal negative C-prefixed entry at the same price. Its positive ranking alone should not be interpreted as completed demand or used to recommend restocking.

## How the analysis defines sales

**One row is an invoice line, not a complete order.** Invoice counts use distinct invoice identifiers.

**Positive-sales value** is Quantity × UnitPrice for product-like lines with positive quantity, positive price, a valid timestamp, and no cancellation prefix. **Signed recorded value** uses the same product-like, positive-price, valid-date scope while retaining signed quantities and cancellation entries. Neither measure is profit or audited net revenue.

The notebook preserves the original DataFrame and documents these choices:

- Remove exact repeated rows as an explicit assumption; without a unique line ID, repetition cannot always be proven accidental.
- Retain missing customer IDs for product and country totals. Those records cannot identify repeat customers.
- Treat codes beginning with five digits as product-like. This heuristic excludes obvious adjustments and some plausible merchandise; it is not a verified product catalogue.
- Exclude nonpositive prices from monetary comparisons rather than silently repairing them.
- Compare January–November 2011 to avoid treating the partial final month as complete.

## Run locally

Use Python 3.11 or newer. From a terminal:

```bash
git clone https://github.com/codingmermaid/exploring-customer-sales.git
cd exploring-customer-sales
python -m venv .venv
```

Activate the virtual environment:

```bash
# macOS / Linux
source .venv/bin/activate
```

```powershell
# Windows PowerShell
.venv\Scripts\Activate.ps1
```

Then install dependencies and open JupyterLab:

```bash
python -m pip install -r requirements.txt
python -m jupyterlab
```

Open `exploringSales.ipynb` and run the cells in order. The first Excel load may take a minute.

## Make the project your own

1. Compare mean and median invoice value in the positive-sales view.
2. Rank countries by unique invoices instead of monetary totals.
3. Repeat the monthly analysis for UK customers only.
4. Recalculate the totals without deduplication and measure the difference.

For your chosen extension, explain what you expected, what you found, and what the data cannot establish.

## Project files

| File | Purpose |
|---|---|
| [`exploringSales.ipynb`](exploringSales.ipynb) | Guided notebook, saved outputs, five charts, and exercises |
| [`images/monthly-sales.png`](images/monthly-sales.png) | Chart extracted from the notebook's saved output |
| [`requirements.txt`](requirements.txt) | Dependencies for running locally |
| [`.gitignore`](.gitignore) | Excludes local environments, caches, and downloaded datasets |

## Data source and limitations

**Chen, D. (2015). Online Retail [Dataset]. UCI Machine Learning Repository.**  
DOI: [10.24432/C5BW33](https://doi.org/10.24432/C5BW33) · [Dataset documentation](https://archive.ics.uci.edu/dataset/352/online+retail) · [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

The source covers December 1, 2010–December 9, 2011. Prices are in GBP, and many customers are wholesalers. This project filters and summarizes the original records as documented in the notebook. The dataset's license applies to the dataset; it is not a separate license grant for the tutorial material.

This is one historical retailer, not a representative sample of all online shoppers. Missing customer identifiers affect customer-level analysis. We have not reconciled transactions with accounts or matched every cancellation to an original purchase. Costs, margins, taxes, and causal explanations are outside the project scope.

The notebook includes saved execution outputs. Restart your runtime and run all cells before relying on your own modified results.
