---
layout: post
title: "Bank Statement Importer for GnuCash, Part 4: Importing Investment Transactions"
categories:
  - Programming
  - Personal Finance
  - GnuCash Importer
image: assets/images/gnucash.webp
description: "Extending the importer to handle stock purchases and sales, including shares, prices, totals, and transaction matching."
---

_This is Part 4 of the Bank Statement Importer for GnuCash series._

- [Part 1: CSV Parsing and Transaction Categorizer]({% post_url 2016-01-07-bank-statement-to-gnucash-1 %})
- [Part 2: Attempting Automated Statement Downloads]({% post_url 2018-10-26-bank-statement-to-gnucash-2 %})
- [Part 3: Carrying Accounts Into a New Year]({% post_url 2019-02-08-bank-statement-to-gnucash-3 %})
- **Part 4: Importing Investment Transactions**

---

The early versions of the Bank Statement Importer for GnuCash worked with ordinary dollar-denominated transactions: purchases, payments, transfers, and
income.

Investment accounts introduced a different kind of transaction.

Buying a stock is not simply money leaving an account. It involves a security, a number of shares, a per-share price, and a total cash value. To import
investment statements properly, the importer needed to understand all of those pieces.

## More Than a Dollar Amount

A typical purchase transaction contains information like this:

```text
Ticker: ABC
Action: Buy
Shares: 10
Price per Share: $25.00
Total Value: $250.00
```

For a normal bank transaction, the important value is usually just the amount of money moving between two accounts. For an investment transaction, the
importer needs to record both sides:

- Cash leaves the investment account
- Shares are added to the stock account
- The transaction records the number of shares purchased
- The share price and total value are retained

## Adding Stock Transactions

The importer was extended to recognize transactions involving securities and create the corresponding GnuCash entries.

This required supporting information that ordinary bank and credit-card transactions did not need:

- The stock ticker or commodity
- The transaction action, such as buy or sell
- The number of shares
- The price per share
- The total value of the transaction
- Any related cash movement

The commodity also needs to exist in the GnuCash book before its shares can be recorded. This builds on the earlier work for creating currencies and
commodities while copying account structures into a new yearly book.

## Keeping the Matcher Useful

The existing transaction matcher still needed to work for investment imports.

Fortunately, investment statement descriptions are often easier to match than ordinary merchant transactions. Ticker symbols are fairly distinct, and words such as `BUY`, `SELL`, `DIVIDEND`, and `REINVEST` provide useful hints about what kind of transaction is being imported.

A simple rule can be much more reliable when the description includes a clear
ticker and action:

```text
"BUY ABC"       → Investments:Brokerage:ABC
"SELL ABC"      → Investments:Brokerage:ABC
"DIVIDEND ABC"  → Income:Investment Income
```

The matching system remains simple text-based logic, but investment transactions tend to give it more structured text to work with.

## From Statements to Investments

With this change, the importer could process CSV exports from investment accounts in addition to bank accounts and credit cards.

It still depends on defined CSV schemas and carefully maintained matching rules. It is not a universal investment importer, and it cannot infer every
financial detail from an arbitrary statement export.

But it can now represent a meaningful new category of transactions: buying and selling shares, rather than only moving dollars between accounts.
