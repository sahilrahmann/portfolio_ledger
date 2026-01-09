# 📊 Portfolio Ledger

A **Python-based portfolio tracking and analysis tool** that helps you understand the *true* performance of your investment portfolio using raw transaction data.

Unlike most brokerage dashboards, this tool gives you **full transparency**, supports **international markets**, and correctly accounts for **cash inflows and outflows** such as monthly investments or withdrawals.

---

## 🚀 Overview

The Portfolio Ledger uses a **simple CSV file** containing your portfolio transactions (BUY, SELL, CASH IN, CASH OUT) to:

- Fetch historical stock prices automatically
- Track daily portfolio value over time
- Support multiple global markets and currencies
- Convert all values to USD for unified analysis
- Provide clean, analysis-ready data for custom financial modeling

---

## ✨ Key Features

- 📄 CSV-based input for all transactions
- 🌍 Supports US 🇺🇸, EU 🇪🇺, UK 🇬🇧, and Japan 🇯🇵 stocks
- 💱 Automatic currency conversion to USD
- 💰 Proper handling of CASH IN / CASH OUT
- 📈 Daily portfolio valuation (stocks + cash)
- 🧪 Ideal for custom analytics and research


---

## ❓ Problems This Library Aims to Solve

Most investors rely on online brokerage platforms to evaluate their portfolio performance. While convenient, these platforms come with several important limitations:

- **Lack of raw data access**: Broker dashboards rarely expose clean, transaction-level data that can be reused for deeper or custom analysis.
- **One-size-fits-all metrics**: Performance metrics are often generic and do not reflect individual investment strategies.
- **Poor handling of cash flows**: Regular cash injections (e.g. monthly investments) and withdrawals are usually ignored or handled incorrectly, leading to misleading return calculations.
- **Fragmented portfolios**: Investors using multiple brokerage accounts cannot easily analyze their portfolio as a single unified entity.
- **Limited analytical flexibility**: Custom analysis such as correlations, risk exposure, drawdowns, or scenario testing is typically not supported.

This library addresses these problems by:

- Using a **simple CSV transaction log** as the single source of truth
- Correctly accounting for **BUY, SELL, CASH IN, and CASH OUT** events
- Producing **daily portfolio valuations** that are transparent and reproducible
- Supporting **multiple markets and currencies**
- Giving users **full control over their data** for advanced analytics and research

The goal is not to replace broker dashboards, but to empower users with **accurate, flexible, and analysis-ready portfolio data**.
---

## 🛠️ Installation

```bash
git clone https://github.com/your-username/portfolio-ledger.git
cd python-portfolio-tracker
conda create --name python-portfolio-tracker --file requirements.txt
conda activate python-portfolio-tracker
```

---

## 📥 Input Data Format

The tracker works entirely from a **CSV file** that contains all portfolio transactions.

Default location:
```
data/raw/purchase_info.csv
```

### Required Columns

| Column | Description |
|------|-------------|
| `date` | Transaction date |
| `action` | BUY, SELL, CASH IN, CASH OUT |
| `company` | Company name |
| `yahoo_ticker` | Yahoo Finance ticker |
| `currency` | USD, EUR, GBP, JPY |
| `num_shares` | Number of shares |
| `stock_price_usd` | Price per share in USD |
| `trading_costs_usd` | Fees |
| `total_usd` | Total transaction value |
| `total_shares_held` | Shares after transaction |

---

### Key Input Rules

- Cash inflows and outflows should be recorded using `CASH IN` and `CASH OUT` in the `action` column.
- The **first row must be `CASH IN`** to define your starting cash balance before any stock purchases.

---

### Example Input Table (Full Sample)

| date       | action   | company                     | yahoo_ticker | currency | num_shares | stock_price_usd | trading_costs_usd | total_usd | total_shares_held |
|------------|----------|-----------------------------|--------------|----------|-----------:|----------------:|------------------:|----------:|------------------:|
| 17/07/2019 | CASH IN  | cash                        | cash         | USD      |          0 |      100000     |              0    | 100000    |                 0 |
| 17/07/2019 | BUY      | Intel                       | INTC         | USD      |        180 |          49.91  |              4.95 |   8988.75 |               180 |
| 17/07/2019 | BUY      | Applied Materials           | AMAT         | USD      |        268 |          45.9151|              4.95 |  12310.2  |               268 |
| 17/07/2019 | BUY      | MKS Instruments             | MKSI         | USD      |        120 |          76.7449|              4.95 |   9214.34 |               120 |
| 17/07/2019 | BUY      | Synopsys                    | SNPS         | USD      |         68 |         136.808 |              4.95 |   9307.92 |                68 |
| 17/07/2019 | BUY      | SOXX ETF                    | SOXX         | USD      |         75 |         204.261 |              4.95 |  15324.5  |                75 |
| 18/07/2019 | BUY      | Nvidia                      | NVDA         | USD      |         39 |         166.67  |              4.95 |   6505.08 |                39 |
| 24/07/2019 | BUY      | Tokyo Electron              | 8035.T       | JPY      |        100 |         168.413 |            126.31 |  16967.7  |               100 |
| 24/07/2019 | BUY      | BE Semiconductor Industries | BESI.AS      | EUR      |        420 |          29.9253|            100    |  12668.6  |               420 |
| 26/11/2019 | SELL     | Nvidia                      | NVDA         | USD      |          5 |         217     |              4.95 |   1089.95 |                34 |
| 25/12/2019 | CASH IN  | cash                        | cash         | USD      |          0 |       10000     |              0    |  10000    |                 0 |
| 25/03/2020 | BUY      | Nvidia                      | NVDA         | USD      |         10 |         205.75  |              4.95 |   2062.45 |                44 |
| 25/05/2020 | CASH OUT | cash                        | cash         | USD      |          0 |        5000     |              0    |   5000    |                 0 |

---

## ▶️ Quick Start

```python
from ppt.portfolio_value import Portfolio

# Load portfolio from the default CSV location
portfolio = Portfolio()

# Daily portfolio value in USD
portfolio.portfolio_value_usd
```

---

## 🧪 Running Tests

```bash
pytest --cov-config=.coveragerc --cov=ppt
```

---

## 📜 License

MIT License
