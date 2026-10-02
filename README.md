# DSA 2050 - Week 2 Practical Lab: SQL, Data Acquisition and Join Validation

**Name:** [Your Name]
**Student ID:** [Your Student ID]
**Lecturer:** Austin Odera

## Objective
This project is the DSA 2050 Week 2 practical lab. It builds three small source datasets (customers, orders and a JSON region lookup) that contain deliberate quality issues, loads them into SQLite, and uses SQL and pandas to filter, aggregate and join the data. The focus is on relational keys and grain: detecting a duplicate customer key and an unmatched order customer, observing how they distort a JOIN, reconciling row counts and sales totals before and after the join, correcting the key problem, and then producing trustworthy segment and regional sales KPIs with short evidence-based interpretations.

## Key Findings
1. **Duplicate key inflated the JOIN.** `CustomerID` `C004` appears twice in `customers.csv`, so order `O005` was duplicated: rows rose from 15 to 16 and total sales from KSh 113,500 to KSh 122,600 (+KSh 9,100). After de-duplicating the customer table, the row count (15) and total (KSh 113,500) reconcile.
2. **Unmatched order.** Order `O015` (KSh 9,900) belongs to `C999`, which does not exist in the customer table. It was kept as an explicit "Unmatched / NULL" group (about 9% of sales) instead of being deleted.
3. **Corporate leads sales, Nairobi leads regions, but with caveats.** Corporate generated the most sales (KSh 46,800) and Nairobi the highest regional sales (KSh 39,800). These are revenue-only figures on a very small dataset, so they do not show profitability or overall best performance.

## Repository Structure
```
DSA2050-Week2-StudentID/
├── DSA2050_Week2_SQL_Lab.ipynb   # full lab: steps, questions, code, outputs and answers
├── customers.csv                 # source data (customers, includes duplicate C004)
├── orders.csv                    # source data (orders, includes unmatched C999)
├── regions.json                  # region lookup
├── requirements.txt
└── README.md
```
`retail_lab.db` (the SQLite database) is created automatically when the notebook runs.

## How to Run
```bash
pip install -r requirements.txt
jupyter notebook DSA2050_Week2_SQL_Lab.ipynb
```
Then choose **Kernel > Restart & Run All**. The notebook regenerates the source files and the database from the top, so no manual setup is needed.
