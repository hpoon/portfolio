---
layout: post
title: "Bank Statement Importer for GnuCash, Part 6: Adding ML Transaction Classification"
categories:
  - Programming
  - Personal Finance
  - GnuCash Importer
image: assets/images/gnucash.webp
description: "Using historical GnuCash transactions to train a classifier that suggests categories for imported bank-statement transactions"
---

_This is Part 6 of the Bank Statement Importer for GnuCash series._

- [Part 1: CSV Parsing and Transaction Categorizer]({% post_url 2016-01-07-bank-statement-to-gnucash-1 %})
- [Part 2: Attempting Automated Statement Downloads]({% post_url 2018-10-26-bank-statement-to-gnucash-2 %})
- [Part 3: Carrying Accounts Into a New Year]({% post_url 2019-02-08-bank-statement-to-gnucash-3 %})
- [Part 4: Importing Investment Transactions]({% post_url 2020-01-04-bank-statement-to-gnucash-4 %})
- [Part 5: Adding a Keyboard-First Review Interface]({% post_url 2021-06-13-bank-statement-to-gnucash-5 %})
- **Part 6: Adding ML Transaction Classification**

---

The earlier versions of the Bank Statement Importer for GnuCash relied on defined CSV formats and text-matching rules.

That worked reasonably well for familiar merchants. A rule for a particular description could pre-populate an account with a fair amount of confidence.
The problem was that every unfamiliar merchant needed another rule, and rules that were too broad could put transactions in the wrong account.

By this point, I had several years of transactions that had already been reviewed and categorised. That gave me something more useful than an expanding
list of string filters: examples of how I had classified similar transactions in the past.

## Training Data

The idea was straightforward: use historical transaction descriptions as input, and the final GnuCash account as the category to predict.

The transaction data was not originally collected as training data, so it needed some rough cleaning first. Descriptions and account assignments had to
be made consistent enough that they could be used as inputs to a classifier.

The intended workflow is still deliberately conservative:

```text
New transaction description
        ↓
Classifier predicts a likely GnuCash account
        ↓
Importer pre-populates the transaction
        ↓
I verify or correct the result
```

The classifier is not making final bookkeeping decisions. It is providing a better first suggestion than the old text matcher could provide on its own.

## Trying Different Models

I tried several classification models:

- Random forest classifier
- Linear SVC
- SVC
- Multinomial naive Bayes
- Logistic regression
- MLP classifier

I do not have a machine-learning background, so this was a practical comparison rather than a rigorous research project. I trained the models on
historical transactions and used cross-validation to see how well they classified examples that were held back from training.

The linear SVC performed best in my tests. It categorised roughly 90 percent of transactions correctly during cross-validation, which was a useful
improvement over relying only on manually maintained text-matching rules.

## Choosing the Features

I also tried giving the models more information than just the transaction description.

For example, I included dollar amounts as an additional feature. In theory, amounts could provide useful hints: a small recurring charge might look
different from a large purchase, and some types of expenses often fall within a predictable range.

In practice, using only the transaction description worked best.

Bank-statement CSV files do not provide many other reliable fields that are useful for categorisation. Amounts turned out to be noisy, and adding them did
not improve the results. The description was the most consistent signal available, which makes sense: it usually contains the merchant name or other
details about the transaction itself.

## A Useful but Imperfect Predictor

A 90 percent result is encouraging, but it does not mean the model understands my finances.

The training data is heavily weighted toward dining and groceries, so those categories appear far more often than others. When the model sees an
unfamiliar or ambiguous description, it has a tendency to choose one of those common categories.

That can produce a good overall accuracy number while still missing less common categories. A model that frequently selects the most common answer can
be right a lot of the time simply because that answer occurs so often.

Fortunately, incorrect predictions are not especially costly here. The importer is only suggesting an account, and I still review transactions before
they are committed to the final GnuCash book. A wrong dining prediction is an annoyance, not a financial decision made without supervision.

## Mostly Verifying Now

The ML matcher now runs when a CSV statement is loaded.

Transactions that receive a confident prediction can arrive with an account already selected. The existing text matcher can still handle especially
obvious descriptions, while the keyboard-first review interface makes it quick to correct anything uncertain.

The project has not become a fully automated bookkeeping system. New merchants, unusual transactions, and incorrect guesses still need review.

But the workflow has changed. Instead of manually categorising every entry, I now find myself mostly verifying the suggestions. That is a substantial
improvement over maintaining text rules and entering account names for every unmatched transaction.

Over time, as I write more transactions, I have opportunity to use new transactions to retrain the model too.
