---
layout: post
title: "Bank Statement Importer for GnuCash, Part 5: Adding a Keyboard-First Review Interface"
categories:
  - Programming
  - Personal Finance
  - GnuCash Importer
image: assets/images/gnucash.webp
description: "Adding a small jQuery-based interface to review and categorise imported transactions more quickly"
---

_This is Part 5 of the Bank Statement Importer for GnuCash series._

- [Part 1: CSV Parsing and Transaction Categorizer]({% post_url 2016-01-07-bank-statement-to-gnucash-1 %})
- [Part 2: Attempting Automated Statement Downloads]({% post_url 2018-10-26-bank-statement-to-gnucash-2 %})
- [Part 3: Carrying Accounts Into a New Year]({% post_url 2019-02-08-bank-statement-to-gnucash-3 %})
- [Part 4: Importing Investment Transactions]({% post_url 2020-01-04-bank-statement-to-gnucash-4 %})
- **Part 5: Adding a Keyboard-First Review Interface**

---

The Bank Statement Importer for GnuCash could already parse CSV files, recognise some transactions, and pre-populate accounts using matching rules.

That still left a manual review step.

Working through unmatched transactions from the command line became tedious. I had to repeatedly type account names, remember shortcuts, and move through
entries one at a time with very little help from the interface. The importer was doing useful work, but reviewing its output was slower than it needed to
be.

## A Small Interface Layer

This version adds a rudimentary web interface on top of the importer.

It is not intended to be a polished personal-finance application. It is a small jQuery-based layer built to make the existing import and review workflow
more practical.

The interface presents imported transactions for review and allows account names to be selected, copied, pasted, or completed without repeatedly typing
the full account path.

## Faster Transaction Review

GnuCash account names can become long, especially when they follow a useful hierarchy:

```text
Expenses:Food:Groceries
Expenses:Home:Utilities:Internet
Assets:Investments:Brokerage
Liabilities:Credit Cards:Main Card
```

Typing those paths repeatedly in a command-line workflow was unnecessary friction.

The interface adds a few practical features:

- Account-name autocomplete
- Copying and pasting account selections between transactions
- Pre-populated account fields for automatically categorised entries
- Keyboard shortcuts for moving through the transaction list
- A workflow designed to avoid reaching for the mouse

The goal was to make the remaining manual review feel less like data entry and more like quickly confirming or correcting the importer's suggestions.

## Keyboard First

The interface was designed so that the review process could be completed using hotkeys alone.

That matters when working through a large statement. Even small delays-moving to the mouse, finding a field, selecting an account, moving back to the next
transaction-become noticeable when repeated dozens or hundreds of times.

A keyboard-first workflow makes it possible to:

```text
Review transaction
        ↓
Accept or change the suggested account
        ↓
Move to the next entry
        ↓
Repeat
```

The importer still cannot determine every category correctly, but the interface makes correcting the uncertain cases much faster.

## Bringing Yearly Setup Into the Interface

The web interface also exposes the yearly book carry-over feature.

Instead of treating the creation of a new GnuCash book as a separate command-line process, the same interface can copy the account tree, required
currencies and commodities, and prior-year balances into the new book.

That brings two recurring tasks into one place:

- Reviewing and importing new transactions
- Preparing the next year's GnuCash book

## A More Useful Tool

This version did not make the importer substantially smarter. The underlying matching logic remains based on defined CSV schemas and text filters.

It made the tool more usable.

Automatically categorised transactions arrive with their account fields already populated. Unmatched or uncertain transactions still need attention,
but reviewing them no longer requires repeatedly entering the same account names in a terminal. The result is a more practical bridge between bank
statements and a completed GnuCash book.
