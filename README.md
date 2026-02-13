![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# Lab | Data Loading and Cleaning in pandas

## Overview

This lab focuses on the practical steps of loading data, checking data quality, and applying cleaning rules in pandas. You will work with a synthetic dataset that simulates customer support tickets, including messy values that require careful handling. The emphasis is on building a clean, reproducible workflow and validating each transformation.

## Learning Goals

By the end of the lab, you should be able to load data into pandas, inspect types and missing values, clean inconsistent fields, and verify that your cleaned dataset is logically consistent. You should also be able to explain why each cleaning step is necessary.

## Setup and Context

You will use the CSV dataset included in this repository: `data_safe_copy.csv`. Each row represents a support ticket with fields `ticket_id`, `opened_at`, `category`, `priority`, and `resolution_minutes`. The dataset includes intentional issues such as missing values, inconsistent casing, and invalid numeric entries. Work in a notebook named `m1-06-loading-cleaning-lab.ipynb`.

## Requirements

- Fork this repository to your own GitHub account.
- Clone your fork to your machine.
- Use the included CSV file `data_safe_copy.csv` from the lab repository.
- Make sure you can open and run Jupyter notebooks (for example via Jupyter Lab or VS Code).

## Getting Started

- Create a new notebook and name it `m1-06-loading-cleaning-lab.ipynb`.
- Confirm you can successfully load `data_safe_copy.csv` before moving on to cleaning steps.
- Before you submit, restart your kernel and run the notebook **top to bottom**.

## Tasks

### Task 1: Generate and load the raw dataset

Load the CSV file `data_safe_copy.csv` into a DataFrame named `tickets`. Confirm that it has at least 500 rows. Print the first five rows and run `info()` to confirm the initial structure.

### Task 2: Parse dates and clean categories

Convert `opened_at` to a datetime column. Then normalize `category` and `priority` by stripping whitespace and converting to lowercase. Show the unique values for both columns to confirm cleaning.

### Task 3: Convert resolution time safely

Convert `resolution_minutes` to numeric values. Invalid entries should become missing values. After conversion, compute the count of missing values and confirm it matches the number of intentionally introduced issues.

### Task 4: Filter and validate cleaned data

Create a cleaned DataFrame named `tickets_clean` by dropping rows with missing `resolution_minutes`. Then verify:
1. All remaining `resolution_minutes` are non-negative
2. All categories and priorities are normalized

Show the number of records before and after cleaning.

### Task 5: Build a quality summary

Create a summary dictionary with keys `total_records`, `clean_records`, `missing_resolution`, `avg_resolution`, and `max_resolution`. Print the summary and verify that `clean_records + missing_resolution` equals `total_records`.

## Common Pitfalls and Debugging Notes

A common mistake is converting `resolution_minutes` before cleaning strings like `"unknown"`, which can produce unexpected errors. Use `pd.to_numeric` with `errors="coerce"` to handle invalid values safely. Another frequent issue is forgetting to strip whitespace in text fields, which leads to duplicate categories that look different but represent the same value.

When validating counts, make sure you are using the correct DataFrame (raw vs. cleaned). Mixing them up can lead to confusing totals.

## Submission

### What to submit

Submit the following files:
- The notebook file `m1-06-loading-cleaning-lab.ipynb`

### Definition of done (checklist)

Before you submit, make sure:

- [ ] The notebook runs **top to bottom** without errors after a kernel restart.
- [ ] You loaded the CSV into `tickets` and verified shape/dtypes with `info()`.
- [ ] Dates are parsed, categories/priorities are normalized, and `resolution_minutes` is converted with invalid values coerced to missing.
- [ ] `tickets_clean` contains only valid, non-missing, non-negative `resolution_minutes` values.
- [ ] Your quality summary is consistent (for example, `clean_records + missing_resolution == total_records`).
- [ ] The notebook is saved and included in your git commit.

### How to submit (Git workflow)

- When you’re done, make sure all changes are saved, then run:

```bash
git add .
git commit -m "Solved m1-06 lab"
git push -u origin HEAD
```

- Make a pull request.
- Paste the link to your pull request in the Student Portal.

## Evaluation Criteria

Your work will be evaluated on correctness, clarity, and structure. Correctness means your cleaning rules are applied consistently and your validation checks pass. Clarity means your code is readable and your variables are named clearly. Structure means the notebook runs cleanly from top to bottom and each task is completed in order with visible outputs.
