---
layout: post
title: "Bank Statement Importer for GnuCash, Part 8: Pasting Bank Pages and Checking the Books"
categories:
  - Programming
  - Personal Finance
  - GnuCash Importer
image: assets/images/gnucash.webp
description: "Importing pasted bank pages instead of statement files, checking imports against the book, learning categories from past books, and a more careful returns report."
---

_This is Part 8 of the Bank Statement Importer for GnuCash series._

- [Part 1: CSV Parsing and Transaction Categorizer]({% post_url 2016-01-07-bank-statement-to-gnucash-1 %})
- [Part 2: Attempting Automated Statement Downloads]({% post_url 2018-10-26-bank-statement-to-gnucash-2 %})
- [Part 3: Carrying Accounts Into a New Year]({% post_url 2019-02-08-bank-statement-to-gnucash-3 %})
- [Part 4: Importing Investment Transactions]({% post_url 2020-01-04-bank-statement-to-gnucash-4 %})
- [Part 5: Adding a Keyboard-First Review Interface]({% post_url 2021-06-13-bank-statement-to-gnucash-5 %})
- [Part 6: Adding ML Transaction Classification]({% post_url 2021-06-15-bank-statement-to-gnucash-6 %})
- [Part 7: Calculating Investment Returns]({% post_url 2023-02-02-bank-statement-to-gnucash-7 %})
- **Part 8: Pasting Bank Pages and Checking the Books**

---

Between Part 7 and now, most of the changes were maintenance: banks changed their CSV formats or their websites, new accounts needed readers, and the
models needed retraining every so often.

This latest round was different. It touched almost every part of the app, so this post covers what changed since Part 7.

## A New Backend and Frontend

The backend moved from Tornado handlers to FastAPI. HTTP routes now live separately from the business logic, which sits in plain service classes that
do not depend on the web framework. That made most of the logic much easier to test.

The frontend is now React and TypeScript with an AG Grid review table. It is built once and served by the backend, so the whole app still runs as a
single process on one port.

## Pasting Pages Instead of Downloading Files

The importer has always been built around statement files: download a CSV from the bank, then load it. Every bank has its own format, and those
formats change without warning. Some accounts do not offer a usable export at all.

The new Accounts page takes a different approach. I open the transaction history page on the bank's website, select everything, copy it, and press
Ctrl+V in the app.

```text
Copied bank web page
        ↓
Work out which account the page is for
        ↓
Page reader for that bank extracts the transactions
        ↓
Same review grid and checks as before
```

Each bank gets its own page reader. Readers were added one bank at a time for chequing accounts, credit cards, brokerage accounts, and retirement plans.
Where the page shows a closing balance, the reader fills it in as well.

Once the readers covered every account I use, the old file import and its parsers were removed. The Accounts page also lists each account with the date
of its last transaction in the book, so it is easy to see which accounts are behind.

## Checking Imports Against the Book

Importing the same transactions twice, or missing a few days between statements, has always been easy to do by accident. The import page now checks
each statement against the book before anything is saved:

- **Possible duplicates:** rows with the same account, the same amount, and a date within a few days of a transaction already in the book. Each book
  transaction can match only one row, so two real identical purchases on the same day are not both flagged unless the book has both.
- **Transfers:** a transfer between two asset accounts is often logged from one side first. Matching transfers up to 7 days apart are flagged too.
- **Gaps and overlaps** between the book's last transaction and the start of the statement.
- **A balance check** against the statement's closing balance, updated live as rows are excluded.

Rows that look already imported are excluded by default when the statement loads, so the usual case needs no clicking.

## Learning Categories From the Books

In Part 6, the classifier was trained on exported transaction files, alongside a list of hand-written text filters. Both are gone.

The categorizer now trains on every yearly GnuCash book directly. It retrains in the background when the app starts and after each save, so corrections
feed straight back into the next import. Suggestions are tried in order:

1. Rules for fund trades.
2. The same description on the same account, when the last two saves agree.
3. The model, which now also sees the account and whose transaction it is. A fund held in several accounts goes to the right one.

Merchants that have never been seen before go to a web search, and then to an LLM that picks an account based on what the merchant is. Rows show that
they are being looked up and update when an answer arrives. Anything I have already edited is left alone.

To measure it, I replayed 2024 to 2026 month by month, training only on what came before each month. About 1 row in 7 needed fixing, down from about 1 in
3 with the old approach.

Travel got some special handling too. Travel purchases are placed on the trip whose dates they fall within, and picking a trip for one row carries over to
the nearby travel rows.

## A More Careful Returns Report

The returns calculator from Part 7 got an audit, and a few things were wrong.

The report now shows three returns side by side, all including dividends:

- **Simple return:** gains over the opening balance plus contributions.
- **Modified Dietz:** gains over capital weighted by how long it was invested.
- **Time-weighted return:** returns chained between every trade and dividend, which removes the effect of when money was added or withdrawn.

The comparison also changed from the price-only S&P 500 index to the S&P 500 total return index. Comparing a portfolio that includes dividends against an
index that does not made the comparison look better than it should have.

Other fixes:

- Contributions, withdrawals, and dividends are converted at the exchange rate on their own date.
- Dividends are counted on their ex-dividend date, so a dividend paid after a partial sale is credited to the shares that earned it.
- Share counts are exact decimals, so selling everything leaves zero instead of a sliver that keeps following the price.
- Prices from Yahoo Finance are split-adjusted, so the adjustment is undone and each split is recorded. The report refuses to run until every split has
  been confirmed as booked correctly.
- Estimated prices for retirement-plan funds are now anchored on actual transaction prices and use total-return references, with a small drift for fees.

## Running GnuCash's Own Reports

At year end, I used to open GnuCash and run the same reports by hand for each person: balance sheet, income statement, and an expenses pie chart, each with
the same settings clicked in every time.

The new Reports page runs those reports with `gnucash-cli` on a copy of the year's book, with the settings filled in. The combined reports can be saved as
standalone HTML pages. The page also summarizes corporation draws over the corporation's fiscal year, which spans two yearly books.

## Smaller Things

- If GnuCash has the book open when saving, the app asks to close it and retry instead of showing an error.
- Typing a category that does not exist offers to create the account.
- Dates are shown in ISO format, along with the book's actual last balance date.

The importer still does not import anything without me looking at it first. But between pasting pages, the book checks, and better suggestions, most of that
looking is now confirming rather than fixing.
