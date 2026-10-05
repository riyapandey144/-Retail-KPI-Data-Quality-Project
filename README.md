# 🛍️ Retail KPI & Data Quality Analysis

> 📊 **A concise assessment of retail data quality and KPI performance**
📅 **Assessment Date:** 5 October 2026  
🔄 **Refresh Cadence:** Daily  
👤 **Decision Owner:** Sales / Operations Manager

## 📌 1. Overview

This project evaluates the **quality and reliability of retail-order data** before using it for KPI reporting.

The dataset contains **12 raw records** and **9 fields**. Data was assessed using five key dimensions:

- 🧩 Completeness
- 🔐 Uniqueness
- ✅ Validity
- 🔄 Consistency
- ⏱️ Freshness

### 🚨 Overall Status: **FAIL — Remediation Required**

- ✅ **5 checks passed**
- ❌ **8 checks failed**
- 📊 **5 records** were eligible for KPI reporting

---

## 📊 2. Dataset Summary

| Metric | Value |
|---|---:|
| Raw Records | **12** |
| Columns | **9** |
| KPI-Eligible Records | **5** |
| Excluded Records | **7** |
| Exact Duplicate Rows | **1** |

### 🔑 Main Fields

`order_id` • `order_date` • `customer_segment` • `city` • `category` • `quantity` • `unit_price` • `discount_pct` • `payment_status`

---

## 🔍 3. Data Quality Findings

| Issue | Finding |
|---|---|
| 🔐 Duplicate | `RT-1004` appears twice |
| 📅 Invalid Date | `RT-1002` uses a non-ISO date |
| ❌ Invalid Date | `RT-1006` contains `2026-13-10` |
| 🔢 Invalid Quantity | `RT-1006` has `-1` |
| 🔢 Invalid Quantity | `RT-1008` contains `'two'` |
| 🏷️ Invalid Discount | `RT-1007` has **105%** discount |
| 🏙️ Missing City | `RT-1005` |
| 🏷️ Missing Discount | `RT-1003` |
| 📅 Missing Date | `RT-1011` |
| ⏱️ Freshness | Latest valid date is **260 days old** |

> ⚠️ Invalid records should be **quarantined and corrected** rather than silently repaired.

---

## 💰 4. KPI Snapshot

| KPI | Value |
|---|---:|
| 🧾 Total Orders | **5** |
| 💵 Gross Sales | **₹8,791.00** |
| 🏷️ Discount Amount | **₹729.35** |
| 💰 Recognized Net Sales | **₹4,514.35** |
| 📦 Units Sold | **9** |
| 🛒 Average Order Value | **₹1,504.78** |
| 💳 Paid Order Rate | **60%** |
| ↩️ Refund Rate | **20%** |
| ❌ Failed Payment Rate | **20%** |
| ⏳ Pending Payment Rate | **0%** |

---

## 📈 5. Key Insights

- 🇺🇸 The dataset requires strong data-quality controls before business reporting.
- 💰 Eligible records generated **₹8,791 gross sales**.
- 🛒 Average Order Value stands at **₹1,504.78**.
- 💳 **60%** of eligible orders were paid.
- ↩️ Refund and failed-payment rates are both **20%**.
- ⏱️ Data freshness is a major concern because the latest valid date is **260 days old**.

---

## 🛠️ 6. Recommended Actions

### 1️⃣ Clean the Source Data
Correct invalid dates, quantities, discounts, and missing values.

### 2️⃣ Investigate Duplicates
Review duplicate order `RT-1004`.

### 3️⃣ Add Automated Validation
Enforce rules for dates, quantities, prices, discounts, and order IDs.

### 4️⃣ Improve Data Freshness
Refresh the source data according to the **daily refresh requirement**.

### 5️⃣ Block Untrusted KPIs
Do not publish production KPIs until critical quality issues are resolved.

## 🏁 7. Conclusion

The analysis shows that the dataset currently **does not meet the required data-quality standards**.

Although the KPI snapshot provides useful business insights, it should be treated as **auditable but not production-trusted** until the identified issues are corrected.

### ✨ Final Takeaway

> **Clean Data 🧹 → Reliable KPIs 📊 → Better Business Decisions 🚀**
