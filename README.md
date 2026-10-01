# Elo Q4 Playbook

An end-to-end analysis of a payment network's transaction data, built to answer one question from the Board:

> Based on everything in this data, what kind of payment network are we, and what should that tell us about where to point the promotions programme in Quarter 4?

The analysis recovers true transaction values from a normalised field, profiles cardholders and merchants, models authorisation risk, and builds a quantitative Q4 promotions targeting map across 23 merchant subsectors — presented as a full written report and as a standalone interactive dashboard.

## What's in this repo

| File | What it is |
|---|---|
| `Elo_Analysis.Rmd` | The full analysis — R Markdown source, code and narrative, organised as a chain of five questions |
| `Elo_Analysis.html` | The knitted report (self-contained; open directly in a browser) |
| `Elo_Analysis.tex` / `Elo_Analysis.log` | LaTeX/PDF build artefacts from knitting the report |
| `elo_analysis.R` | The analysis as a plain R script |
| `dashboard.html` | Standalone executive dashboard summarising the report's findings (open directly in a browser, no server needed) |
| `figures/` | Exported chart images from the report |
| `Case Study of Elo.docx` | Narrative write-up of the case study |
| `Elo.pptx` | Presentation deck |
| `Data/Data Dictionary.xlsx` | Field definitions for the raw data |
| `Data/` | Raw data, included in this repo — see below |

## Data

This project uses the [Elo Merchant Category Recommendation](https://www.kaggle.com/competitions/elo-merchant-category-recommendation) dataset from Kaggle: a historical transaction ledger (`historical_transactions_100k.csv`), a new-merchant transaction window (`new_merchant_transactions.csv`), and a merchant reference table (`merchants1.csv`), plus the competition's own `Data Dictionary.xlsx`.

The raw CSV files are included in `Data/` for reproducibility. The dataset itself remains subject to Kaggle's own competition terms, separate from this repo's MIT license (see [License](#license)) — check the competition page above before reusing the data elsewhere. To reproduce the analysis, run `Elo_Analysis.Rmd` (or `elo_analysis.R`) from the project root; it reads directly from `Data/`.

## Key findings

- **Currency recovery.** `purchase_amount` ships normalised (roughly −0.75 to +11,270). It's recovered to real Reais via `BRL = purchase_amount ÷ 0.00150265 + 497.06`, validated against the shape of the resulting distribution (no negative amounts, an economically coherent median).
- **Network identity.** 96.1% of transactions settle without a multi-month instalment plan and the median ticket is R$34.90 — a high-frequency, small-ticket, everyday-spend network, not an instalment one.
- **Portfolio concentration.** The top 20% of cards carry 57.7% of spend. Four cardholder segments — Core Everyday, Big-Ticket Narrow, Explorer Light, Occasional — split the base on spend and merchant breadth, cross-checked against an independent k-means clustering.
- **Authorisation.** 93.00% of transactions are approved overall, but an anonymised flag (`category_1 = Y`, 6.1% of volume) carries 4.25× the odds of a decline — the strongest driver in the model, ahead of ticket size or instalment plan.
- **Growth.** The network grows by adding cards (241 → 398 active cards across the window), not by deepening usage per card (which stays roughly flat).
- **Merchants.** 991 Tier-A merchants (0.3% of the base) carry 26.1% of incumbent volume; the top 1,000 merchants carry 50.3% of all transactions. 82.4% of the 334,633-merchant reference file never transacts in either window.
- **Geography.** State 9 is the most under-served market (39% of demand, 28% of merchant supply). State 22 is the cleanest greenfield for merchant acquisition (novelty index 1.31 on thin supply).
- **Discovery.** A first visit to a new merchant runs 40% higher in ticket size than a known one, and instalment use nearly doubles — discovery is a considered purchase, not an impulse one.
- **Q4 targeting map.** Every merchant subsector scored on a Novelty Capture Index and a Coverage Index, splitting the network into acquisition engines, under-supplied habit anchors, and a small over-served quadrant — the basis for the Q4 recommendations in the full report.

## Viewing the dashboard

Open `dashboard.html` directly in any modern browser — it's a single static file with no build step or server required.

## What this analysis cannot tell you

No card-level loyalty file was in the export; the two transaction windows are different card samples (only 16 cards in common); 463 cards is a small panel for state × subsector cross-cuts; subsector identities are anonymised; the currency transform is empirically recovered, not supplied; and the targeting map shows correlation, not proven causation — see the full report for details.

## License

The code, analysis, and written content in this repository are licensed under the [MIT License](LICENSE). This license does not extend to the Kaggle competition dataset, which is not included here and remains subject to its own terms on Kaggle.
