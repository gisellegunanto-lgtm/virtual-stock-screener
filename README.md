# Virtual Stock Screener

A Python script that screens S&P 500 stocks using a mix of relative strength, trend and valuation filters. It pulls one year of price data, ranks each stock against the index, and outputs a shortlist that passes every condition.

## How it works

1. **Get the universe.** Scrapes the current list of S&P 500 tickers from Wikipedia.
2. **Download prices.** Fetches one year of daily data for each ticker and for the index (`^GSPC`) using yfinance, with retries for failed downloads. Each stock's data is saved to `stock_data/`.
3. **Rank relative strength.** Compares each stock's one-year return to the S&P 500's return, converts that to a percentile score (0-100), and keeps the top 30%.
4. **Apply the screen.** A stock makes the final list only if it meets all five conditions:

| Condition | Rule |
|---|---|
| Uptrend | Price > 150-day SMA > 200-day SMA |
| Off the lows | Price is at least 30% above its 52-week low |
| Near the highs | Price is within 25% of its 52-week high |
| Valuation | Trailing P/E below 40 |
| Growth-adjusted valuation | PEG ratio below 2 |

5. **Output.** Results print to the terminal sorted by relative strength score and save to `final.csv`.

## Sample output

| Ticker | Latest_Price | Score | PE_Ratio | PEG_Ratio | SMA_150 | SMA_200 | 52_Week_Low | 52_Week_High |
|---|---|---|---|---|---|---|---|---|
| ... | ... | ... | ... | ... | ... | ... | ... | ... |

<!-- Replace this table with a real run, or add a screenshot: ![Results](screenshot.png) -->

## Installation

Requires Python 3.9 or later.

```bash
git clone https://github.com/gisellegunanto-lgtm/virtual-stock-screener.git
cd virtual-stock-screener
pip install pandas yfinance requests lxml
```

## Usage

```bash
python "Virtual Stock Screener.py"
```

A full run checks about 500 tickers and takes several minutes, depending on your connection.

## Tech stack

- Python
- pandas for data handling and rolling averages
- yfinance for price and fundamentals data
- requests for scraping the ticker list

## Disclaimer

This project is for learning purposes. It is not financial advice.
