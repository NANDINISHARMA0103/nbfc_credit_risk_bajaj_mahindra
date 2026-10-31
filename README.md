# Credit Analysis of NBFCs: Bajaj Finance vs Mahindra Finance

A ten-year (FY2016-17 to FY2025-26) comparison of two Indian non-banking finance companies, **Bajaj Finance** and **Mahindra & Mahindra Financial Services**, with a focus on asset quality, credit cost, profitability, capital, liquidity and the risk of their loan segments.

Done as part of my MSc Economics coursework at Symbiosis School of Economics, Pune.

---

## Project at a glance

| | |
|---|---|
| **Question** | How do Bajaj Finance and Mahindra Finance compare on credit quality and risk, and what explains the difference? |
| **Period** | FY2016-17 to FY2025-26 (10 years; FY2015-16 is used only as an opening base for averages and growth) |
| **Companies** | Bajaj Finance (consolidated), Mahindra Finance (standalone) |
| **Framework** | The 7 Cs of credit analysis (see the report) |
| **Tools** | Python (pandas, numpy), Excel, PowerPoint |

## Repository contents

```
nbfc-credit-analysis/
├── README.md
├── requirements.txt
├── data/
│   ├── raw/
│   │   ├── Bajaj_Finance_10yr_Dataset.xlsx     # source data, Bajaj
│   │   └── Mahindra_Data.xlsx                  # source data, Mahindra
│   └── processed/
│       ├── NBFC_merged_final.xlsx              # merged, cleaned master dataset
│       └── NBFC_dashboard_ready.xlsx           # summary tables used for charts and slides
├── notebooks/
│   ├── Financial_Assignment.ipynb              # data cleaning, imputation, ratio building
│   └── NBFC_Credit_Analytics.ipynb             # analysis and charts
└── reports/
    ├── Bajaj_vs_Mahindra_7Cs_Combined.pdf      # written report
    └── <your_presentation>.pptx                # presentation slides
```

## What each file does

- **`Financial_Assignment.ipynb`** reads the two raw Excel files and builds one company-by-year panel. It standardises column names, converts ratios to percentages, fills gaps using documented rules (every filled cell is logged), calculates ratios, builds a segment table with risk tiers, runs consistency checks, and exports the master dataset.
- **`NBFC_Credit_Analytics.ipynb`** uses the cleaned data for analysis and charts.
- **`NBFC_merged_final.xlsx`** is the merged master dataset (panel and segments).
- **`NBFC_dashboard_ready.xlsx`** holds the cleaned summary tables behind the charts.
- **`Bajaj_vs_Mahindra_7Cs_Combined.pdf`** is the full written analysis.
- **The presentation** summarises the findings. The README explains the repository itself; the slides explain the findings.

## Main variables

Asset quality: GNPA %, NNPA %, provision coverage ratio, Stage 2 and Stage 3 share, ECL to loans.
Credit cost: credit cost % of average AUM, write-off ratio.
Profitability and efficiency: ROA, ROE, operating cost to net total income, impairment to net total income.
Capital and leverage: CRAR, Tier 1, leverage, debt-to-equity, NNPA to net worth.
Liquidity: LCR, liquidity buffer to AUM.
Segment risk: share of high-risk and unsecured assets.

(Add a full data dictionary under `docs/` if you want one.)

## Key observations

Checked against the master dataset:

- Mahindra's reported GNPA fell from about 9.0% (FY17) to 2.9% (FY26). Bajaj's stayed in the 0.85% to 1.8% range.
- Bajaj's share of high-risk segments fell from about 65% (FY17) to about 37% (FY26). Mahindra's rose from about 23% to 33%.
- Credit cost peaked for both in FY2020-21 (COVID year).

*(Replace or extend these with the conclusions from your report and slides.)*

## How to run

1. Open `notebooks/Financial_Assignment.ipynb` in **Google Colab**.
2. Run the first cell and upload both files from `data/raw/` when asked. The notebook uses Colab's `files.upload()`, so it will not run unchanged on a local machine.
3. Run all cells in order. The notebook writes `NBFC_master_dataset.xlsx` and `NBFC_master_panel.csv`.
4. Open `NBFC_Credit_Analytics.ipynb` and run it the same way.

Requirements: Python 3.9+, `pandas`, `numpy`, `openpyxl`. Install with `pip install -r requirements.txt`.

## Data sources

Company annual reports, investor presentations and regulatory disclosures of Bajaj Finance Ltd and Mahindra & Mahindra Financial Services Ltd. *(Add exact documents and years if you can.)*

## Important caveats

Please read before using the numbers.

- **Different reporting bases.** Bajaj is consolidated; Mahindra is standalone. The `Basis` column records this.
- **Estimated Bajaj balance sheet, FY2020-21 to FY2025-26.** Net worth is estimated from reported ROE and PAT, total assets from equity times reported leverage, and borrowings from total assets. These rows are flagged with `BS_estimated = 1`, and ROE/ROA recalculated from them are left blank to avoid circular logic.
- **Estimated write-offs.** Missing Bajaj write-offs come from an ECL roll-forward (opening ECL + impairment charge − closing ECL). Against years with reported figures it was within about 3%, with the largest gap (about 3%) in FY2020-21.
- **Mahindra segment GNPA is modelled, not disclosed.** It is allocated from total Gross NPA using risk weights (Low 0.5, Medium 1.0, Medium-High 1.5, High 2.0). These weights and the segment risk tiers are my own judgement. Rows are flagged `GNPA_is_modelled = 1`.
- **Comparability.** NPA recognition norms changed over the period (4-month, then 3-month, then strict 90 days past due). The `NPA_norm` column flags this. Stage 1 and 2 data do not exist before Ind AS, and LCR only began in December 2020, so those cells are blank by design.
- **Known data checks.** Mahindra's stage totals differ from its loan base by more than 2% in six years, and its calculated GNPA differs from the reported value by more than 0.5 percentage points in FY2020-21.

## Author

[Your name], MSc Economics (2025-27), Symbiosis School of Economics, Pune
[Your email or LinkedIn]

## License

Code is released under the MIT License. Source data belongs to the respective companies and is used for educational purposes.
