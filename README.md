# Data Analytics Assessment

This repository contains solutions to a four-question SQL assessment designed to evaluate data analytics and SQL skills using a financial transactions dataset.

---

## ✅ Question 1: High-Value Customers with Multiple Products

### Goal:
Identify customers who own at least one **funded savings plan** and one **funded investment plan**.

### Approach:
- Used conditional self-joins on `plans_plan` to isolate savings (`is_regular_savings = 1`) and investments (`is_a_fund = 1`).
- Aggregated deposits using `savings_savingsaccount` and filtered funded plans.
- Sorted by total deposit amount.

### Assumptions:
- `confirmed_amount` is in kobo, hence divided by 100.
- Same customer can have multiple plan types.

---

## ✅ Question 2: Transaction Frequency Analysis

### Goal:
Classify customers by monthly transaction frequency.

### Approach:
- Aggregated transactions per customer per month.
- Averaged per user using CTEs.
- Applied `CASE` to categorize into "High", "Medium", and "Low" frequency bands.

### Assumptions:
- `date_created` exists and reflects transaction date.

---

## ✅ Question 3: Account Inactivity Alert

### Goal:
Flag accounts (savings or investments) with no transactions in the last 365 days.

### Approach:
- Combined savings and investment accounts using `UNION`.
- Used `MAX(date_created)` to identify last inflow.
- Filtered out recent activity.

### Assumptions:
- Accounts with `confirmed_amount > 0` are considered "active".

---

## ✅ Question 4: Customer Lifetime Value (CLV)

### Goal:
Estimate CLV using transaction volume and account tenure.

### Formula:
\[
CLV = \left(\frac{\text{total_transactions}}{\text{tenure_months}}\right) \times 12 \times \text{avg_profit_per_txn}
\]

### Approach:
- Extracted tenure from `date_joined`.
- Aggregated transaction counts and average value.
- Applied formula assuming `0.1%` profit per transaction.

---

## 🔍 Challenges

- Some assumptions about schema (like date fields and identifiers) were made due to the SQL dump format.
- Handling zero-tenure edge cases to avoid division by zero.
- Ensuring proper unit conversions from kobo to Naira.

---

## 📝 Notes

- All queries were tested for clarity, performance, and accuracy.
- CTEs were used for readability and modular design.
