---
layout: post
title: "Bank Statement Importer for GnuCash, Part 1: CSV Parsing and Transaction Categorizer"
categories:
  - Programming
  - Personal Finance
  - GnuCash Importer
image: assets/images/gnucash.webp
description: "The first step in an ongoing project to import bank and credit-card statements into GnuCash with automatic transaction categorization"
---

As I got more bank accounts for different things like chequing, savings, credit cards, investments, etc., it got harder to keep track of where I was financially. So this is where I began to need a way to track my personal finances as a whole. There are tools like Mint.com that helps people track their financial data. I never liked the idea of sharing my financial data with another service in the cloud. A local solution is GnuCash (of course there are paid options, but this one is FOSS)

Keeping financial records up to date is simple in theory: download a statement, import the transactions, and categorize them. In practice, every bank exports its CSV files a little differently, and the same familiar transactions need to be categorized again and again. GnuCash can
import CSV files, but the categorization is a manual effort.

This project is a small piece of software that reads statement exports from several bank accounts and credit cards, normalizes them, applies rules based on what I already know about the transactions, and produces data ready for GnuCash.

## The Goal

The goal was not to replace GnuCash or build a full personal-finance platform.

It was to create a practical layer between bank-provided CSV files and GnuCash:

```text
Bank or credit-card CSV
        ↓
Parser for that institution
        ↓
Normalized transaction data
        ↓
Matching and categorization rules
        ↓
Import into GnuCash using Python bindings
```

The important part is the matching step. A transaction description can often tell me enough to identify where it belongs: a known merchant, subscription,
utility, transfer, payment, or recurring expense.

## The First Version

The initial version supported several of my bank accounts and credit cards.

Each account had its own input format, so the importer needed to handle differences in column names, dates, transaction descriptions, amounts, and
whether debits and credits were represented as separate columns or a signed amount.

After parsing, transactions were converted into a common internal format before any categorization rules were applied.

## Matching Transactions

The first categorization system was intentionally simple: a lookup table based on string matching.

Conceptually, it looked like this:

```text
"NETFLIX"        → Expenses:Subscriptions
"SPOTIFY"        → Expenses:Subscriptions
"WHOLE FOODS"    → Expenses:Groceries
"PAYROLL"        → Income:Salary
```

If a transaction description contained a known string, the importer could pre-populate the destination GnuCash account. It did not need to be clever. It
only needed to remove the repeated manual categorization of transactions I already recognized.

Unmatched transactions could remain uncategorized for review, rather than being assigned somewhere with false confidence.

## Why Not Just Import CSVs?

GnuCash already provides CSV-import tools, and they are useful. This project was about adding a layer of personal context that a generic importer cannot
know.

The bank may know that a charge came from a merchant. It does not know how I want that transaction represented in my accounts. Over time, a small set of
rules can capture that knowledge and make future imports faster and more consistent.

## Limitations

Overall, the software isn't that smart. It only reads CSVs that I've defined a schema for, and the simple text search is only as good as the text filters I use. Occasionally, things get filed to the wrong place because the string I used wasn't specific enough. And as I make transactions at new places, they are missing from the filters and so it means I always have to play catch up with the filters - and of course, not all things can be easily filtered. Still, a chunk of transactions get auto flagged. I also have to automatically download each bank statement for import.

Working through unmatched transactions purely from acommand line is also tedious. I have to repeatedly type account names, remember shortcuts, and move through entries one at a time with very little help from the interface. The importer was doing useful work, but reviewing its output was slower than it needed to be.

## The Limits of Simple Matching

The first version is not especially smart.

It only understands CSV formats I have explicitly defined. A new bank, credit card, or export format needs a parser before it can be imported. The
categorization logic is also just text matching, which means it is only as reliable as the filters behind it.

That creates a few predictable failure modes:

- A matching string can be too broad and send a transaction to the wrong account
- A new merchant may not match anything and require a new rule
- Some transactions do not have enough useful description text to categorize confidently
- Transfers, unusual purchases, and one-off expenses often still need manual review

In practice, that meant periodically playing catch-up: reviewing unmatched transactions, correcting mistakes, and adding filters for places I had not
seen before.

Even so, the importer could automatically flag or categorize a meaningful portion of routine transactions. It did not eliminate review, but it reduced
the repetitive part of importing statements into GnuCash.
