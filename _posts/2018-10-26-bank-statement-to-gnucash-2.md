---
layout: post
title: "Bank Statement Importer for GnuCash, Part 2: Attempting Automated Statement Downloads"
categories:
  - Programming
  - Personal Finance
  - GnuCash Importer
image: assets/images/gnucash.webp
description: "An attempt to automate bank-statement downloads for a GnuCash import workflow, and why browser automation was not a long-term answer"
---

- [Part 1: CSV Parsing and Transaction Categorizer]({% post_url 2016-01-07-bank-statement-to-gnucash-1 %})
- **Part 2: Attempting Automated Statement Downloads**

---

The first version of my GnuCash importer handled a useful part of the process: take a downloaded CSV file, normalize its data, apply transaction-matching
rules, and prepare it for import.

It still depended on one manual step: signing in to each financial institution, finding the export page, and downloading the CSV files.

That step became tedious quickly enough that I tried to automate it.

## The Missing API

As an ordinary account holder, I did not have a direct bank API that I could use to request my own transaction exports programmatically.

The banks already provided the information through their websites, but the normal flow was designed for a person using a browser—not a small personal
script retrieving CSV files on a schedule.

So the next version used Selenium to automate the browser steps:

```text
Open bank website
        ↓
Sign in
        ↓
Navigate to transaction history
        ↓
Select the export range and format
        ↓
Download the CSV
        ↓
Pass it to the importer
```

## Browser Automation

The automated flow could handle the repetitive navigation, but it was not fully unattended.

I still had to intervene when a site required a two-factor authentication code. That was an acceptable boundary: the script could reduce repeated clicking, while authentication remained under my control.

When it worked, the approach was convenient. I could start the process, handle the authentication prompt when necessary, and let the importer continue after the CSV files arrived.

## Why It Was Fragile

Selenium is useful for testing websites and automating browser interactions, but it was a poor foundation for a long-lived personal banking workflow.

The automation depended on page structure, button labels, loading behaviour and download flows remaining consistent. A small change to a bank website
could break a selector or send the browser somewhere unexpected. Timing could also be unreliable: a page might load more slowly than usual, a prompt might
appear, or an element might not be ready when the script expected it.

The result was an improvement over manual downloading when it worked, but not reliable enough to become invisible infrastructure.

## The Password-Manager Question

I also considered using a wrapper around my password manager's API so the automation could retrieve credentials as needed.

Technically, that would have been more convenient than manually entering or copying them into the browser flow. But it would also create a new connection
between the automation project and my password-manager account.

I decided I did not want to the system to access highly sensitive credentials.

## Where That Left Things

The browser automation was a useful experiment, but not a dependable solution.

It confirmed that the real friction in the workflow was not CSV parsing or categorization. It was data retrieval: every institution has its own login
flow, export process, security controls, and tendency to change its website without warning.

For now, downloading the files manually remains more reliable. The importer can still save time after that point, and the automation attempt clarified
which parts of the process are worth simplifying—and which parts are better left deliberately manual.
