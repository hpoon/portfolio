---
layout: post
title: "Bank Statement Importer for GnuCash, Part 3: Carrying Accounts Into a New Year"
categories:
  - Programming
  - Personal Finance
  - GnuCash Importer
image: assets/images/gnucash.webp
description: "Adding a way to copy an account structure, currencies, commodities, and opening balances into a new yearly GnuCash book"
---

_This is Part 3 of the Bank Statement Importer for GnuCash series._

- [Part 1: CSV Parsing and Transaction Categorizer]({% post_url 2016-01-07-bank-statement-to-gnucash-1 %})
- [Part 2: Attempting Automated Statement Downloads]({% post_url 2018-10-26-bank-statement-to-gnucash-2 %})
- **Part 3: Carrying Accounts Into a New Year**

---

For a while, the automated statement-download workflow worked well enough.

When the browser automation cooperated, it could navigate through the usual login and download steps. When it did not, I would download the CSV files
manually and let the rest of the importer do its job. It was not fully automatic, but it still reduced some of the repetitive work.

Then a different annual problem showed up.

## Starting a New Book

I keep a separate GnuCash book for each year.

I do not know whether that is how formal accounting workflows are normally structured, but it works for me. A new year starts with a clean set of
transactions while preserving the account structure I use to organize income, expenses, assets, liabilities, and investments.

The problem was that a blank book is very blank.

Every year, I needed to recreate the same account tree, currencies, and commodities. I could copy the previous year's book, remove its transactions,
and use that as a starting point, but that was tedious and made it too easy to leave behind something I did not intend to carry forward.

## Copying the Account Tree

GnuCash accounts are organized as a tree.

A top-level account may contain several child accounts, and those accounts may
have their own children. For example:

```text
Assets
├── Chequing
├── Savings
└── Investments
    ├── Brokerage
    └── Retirement

Expenses
├── Groceries
├── Utilities
└── Subscriptions
```

The new feature walks the previous book's account tree and recreates it in the new book.

Conceptually, this is a depth-first search:

```text
Copy account
    ↓
Create required currency or commodity
    ↓
Create matching account in the new book
    ↓
Copy the account's opening balance
    ↓
Repeat for each child account
```

The account tree is simple to describe, but copying it correctly requires more than creating accounts with the same names.

## Currencies and Commodities

Accounts can be denominated in different currencies or associated with commodities such as stocks.

Before an account can be created in the new book, its currency or commodity must exist there as well. The importer therefore checks whether the required
currency or commodity already exists and creates it when necessary before creating the associated account.

That avoids ending up with an account tree that looks correct but lacks the information required to represent balances properly.

## Carrying Forward Balances

Creating the account structure is only half the job.

The new book also needs starting balances that reflect the end of the previous year. The migration feature copies those balances into the corresponding
accounts in the new book, providing a useful starting point without carrying over the previous year's transaction history.

The result is a new yearly book with:

- The same account hierarchy
- Required currencies and investment commodities
- Opening balances based on the prior year's ending balances
- No need to manually rebuild the entire structure

## A Better Yearly Reset

This feature does not make the project smarter in the way that transaction matching does. It simply removes another recurring piece of setup work.

The first versions focused on getting transactions into GnuCash. This one focuses on making it easier to start the next book without rebuilding the
accounting structure from scratch every January.
