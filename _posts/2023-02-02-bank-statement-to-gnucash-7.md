---
layout: post
title: "Bank Statement Importer for GnuCash, Part 7: Calculating Investment Returns"
categories:
  - Programming
  - Personal Finance
  - GnuCash Importer
image: assets/images/gnucash.webp
description: "Fetching investment prices, estimating retirement-fund values, and calculating returns across multiple years."
---

_This is Part 7 of the Bank Statement Importer for GnuCash series._

- [Part 1: CSV Parsing and Transaction Categorizer]({% post_url 2016-01-07-bank-statement-to-gnucash-1 %})
- [Part 2: Attempting Automated Statement Downloads]({% post_url 2018-10-26-bank-statement-to-gnucash-2 %})
- [Part 3: Carrying Accounts Into a New Year]({% post_url 2019-02-08-bank-statement-to-gnucash-3 %})
- [Part 4: Importing Investment Transactions]({% post_url 2020-01-04-bank-statement-to-gnucash-4 %})
- [Part 5: Adding a Keyboard-First Review Interface]({% post_url 2021-06-13-bank-statement-to-gnucash-5 %})
- [Part 6: Adding ML Transaction Classification]({% post_url 2021-06-15-bank-statement-to-gnucash-6 %})
- **Part 7: Calculating Investment Returns**

---

I now anted to answer: how well are my investments actually performing over time?

GnuCash includes reports that can calculate investment performance for a given year. The difficulty was that those reports depend on security prices being
available in the price database. Without prices, there is no reliable way to calculate the value of a holding at the beginning and end of a period.

## The Price Problem

GnuCash has a price updater, but it was not a complete solution for my portfolio.

It works best for securities with publicly traded ticker symbols. That is fine for common stocks, ETFs, and many mutual funds. It becomes more difficult for funds inside employer retirement plans, where the available funds may be internal plan options rather than securities that can be looked up directly by ticker.

For those investments, updating prices could become a manual data-entry task. That is manageable once or twice, but it is not a good process for calculating returns across several years.

## Fetching Market Prices

This version adds the ability to retrieve ticker prices from Yahoo Finance.

I used a Yahoo Finance API available through RapidAPI to query historical prices for investments with ticker symbols. Those prices can then be added to
the investment data and used to value holdings over time.

The general flow looks like this:

```text
Investment transactions
        +
Historical ticker prices
        ↓
Value of each holding at different points in time
        ↓
Rate of return calculations
```

For securities that have a public ticker, this removes much of the manual work of keeping the GnuCash price database current.

## Estimating Retirement-Fund Prices

Retirement-plan funds were more complicated because some did not have ticker symbols or directly available public price histories.

In my case, several of those funds broadly tracked the S&P 500. That made it possible to estimate their prices using the price movement of the index.

The account history still contained useful information. Dividend transactions provided known points in time where the fund's approximate value could be
anchored. Using those points, I could estimate prices based on changes in the S&P 500 between them.

```text
Known retirement-fund value
        +
S&P 500 movement over time
        ↓
Estimated retirement-fund price
```

This is an approximation, not an official historical fund price. The fund may not track the index perfectly, and fees, cash holdings, or other investment
choices can create differences.

Still, the estimated values were "close enough" to the actual account balances to be useful for analysing longer-term returns.

## Calculating Returns

Once the price data was available, I could calculate the value of each investment across different years.

The rest of the process was less glamorous: a series of multiplications, divisions, dates, and table operations. Pandas made that manageable by keeping
the transactions, prices, quantities, and calculated values together in tabular form.

Comparing those values over time makes it possible to calculate the rate of return for each investment across years and to compare my portfolio performance against the S&P 500.

## Good Enough for Analysis

The result is not a replacement for official brokerage or retirement-plan statements.

Some securities have directly retrieved historical prices. Others use estimated prices based on the available transaction history and an index that
approximately tracks the underlying fund. The estimates are only as good as those assumptions.

But the results are close enough to the reported account balances to make the analysis useful. Instead of seeing only transaction history, I can now use the same data to review investment values and returns over multiple years.
