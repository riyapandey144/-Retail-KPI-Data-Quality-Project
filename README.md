🛍️ Retail KPI & Data Quality Analysis Report
A structured assessment of retail-order data quality and KPI readiness
📅 Assessment Date: 5 October 2026
🔄 Refresh Cadence: Daily
👤 Decision Owner: Sales / Operations Manager
🗂️ Data Owner: Data / Operations Team

📌 1. Executive Summary
This project evaluates the quality, reliability, and KPI readiness of a retail-order dataset containing 12 raw records and 9 fields.
The analysis applies defined rules for completeness, uniqueness, validity, consistency, and freshness before calculating business KPIs. The assessment identifies several source-data issues, including duplicate order IDs, invalid or missing dates, missing city and discount information, invalid quantities, and stale data.
🚨 Overall Data Quality Status: FAIL — Remediation Required
Out of 13 quality checks:
- ✅ 5 checks passed
- ❌ 8 checks failed
- 📊 Only 5 records qualified for the KPI snapshot.
- 🚫 7 records were excluded from KPI calculations.
The KPI snapshot is therefore auditable and useful for project analysis, but it is not production-trusted until the identified source-quality issues are remediated.
📊 2. Dataset Profile
The retail dataset contains the following core transaction fields:
Field	Business Purpose
🆔 order_id	Unique order identifier
📅 order_date	Date on which the customer placed the order
👥 customer_segment	Customer segment
🏙️ city	Customer billing city
🛒 category	Product family
🔢 quantity	Units purchased
💰 unit_price	Price per unit before discount
🏷️ discount_pct	Percentage discount applied
💳 payment_status	Latest order settlement state


📈 Dataset Summary
Metric	Value
Raw Records	12
Columns	9
Unique Order IDs	11
Exact Duplicate Rows	1
KPI-Eligible Records	5
Excluded Records	7


🔍 3. Data Quality Assessment
The project evaluates data against predefined acceptance standards.
🧪 Quality Dimensions
Dimension	Acceptance Standard	Status
🧩 Completeness	Critical IDs 100%; required fields ≥98%; city ≥99%	❌
🔐 Uniqueness	order_id must be 100% unique	❌
✅ Validity	Dates, quantities, prices, discounts and categories/statuses must follow defined rules	❌
🔄 Consistency	Core transaction validity ≥98%	❌
⏱️ Freshness	Latest valid ISO order date must be ≤1 day old	❌


📌 The quality contract requires failed records to be quarantined or corrected rather than silently repaired. Production KPI refresh should be blocked when core consistency falls below the defined threshold.

📋 4. Detailed Quality Results
Quality Check	Pass Rate	Threshold	Status
🆔 Order ID Completeness	100%	100%	✅ PASS
🔐 Order ID Uniqueness	91.67%	100%	❌ FAIL
📅 Order Date Completeness	91.67%	98%	❌ FAIL
📅 Order Date Validity	75%	98%	❌ FAIL
🏙️ City Completeness	91.67%	99%	❌ FAIL
👥 Customer Segment Validity	100%	100%	✅ PASS
🛒 Category Validity	100%	100%	✅ PASS
🔢 Quantity Validity	83.33%	98%	❌ FAIL
💰 Unit Price Validity	100%	100%	✅ PASS
🏷️ Discount Validity	83.33%	98%	❌ FAIL
💳 Payment Status Validity	100%	100%	✅ PASS
🔄 Core Consistency	50%	98%	❌ FAIL
⏱️ Freshness	0%	100%	❌ FAIL


📌 Result
5 of 13 checks passed, while 8 failed. The overall dataset therefore does not satisfy the defined quality contract.
⚠️ 5. Key Data Issues
The analysis identified the following record-level problems:
Record	Issue	Recommended Treatment
🔴 RT-1004	Exact duplicate order row	Keep one copy only for temporary KPI calculation and investigate source duplication
🔴 RT-1002	Date 03/01/2026 is not in required ISO format	Standardize upstream to YYYY-MM-DD and quarantine until corrected
🔴 RT-1003	Missing discount	Do not assume zero without documented business justification
🔴 RT-1005	Missing city	Correct source; exclude from city-level reporting
🔴 RT-1006	Invalid date 2026-13-10	Quarantine and correct source
🔴 RT-1006	Negative quantity -1	Quarantine and correct source
🔴 RT-1007	Discount of 105%	Quarantine and correct source
🔴 RT-1008	Quantity recorded as 'two'	Convert only after validated source correction; quarantine meanwhile
🔴 RT-1011	Missing order date	Quarantine from date-based reporting until corrected
⏱️ Dataset	Latest valid ISO date is 2026-01-18	Refresh source and escalate because freshness SLA is breached


💡 6. Missing-Value Analysis
Three fields contain missing values:
Field	Missing Records	Missing %
📅 order_date	1	8.33%
🏙️ city	1	8.33%
🏷️ discount_pct	1	8.33%


📝 Interpretation
Although the missing-value percentage appears relatively small, these fields have direct business relevance. In particular:
- Missing order dates affect time-based reporting.
- Missing city values reduce the reliability of geographic analysis.
- Missing discounts can affect sales and discount calculations and should not automatically be treated as zero.
🔐 7. Duplicate Analysis
The dataset contains:
- 1 exact duplicate row
- 2 records sharing the same order_id
- Duplicate order ID: RT-1004
The quality contract treats duplicate order IDs as a source-quality failure, even if one copy is removed temporarily for a KPI snapshot.
🛑 Deduplication for analysis does not eliminate the underlying source-quality problem.

📅 8. Freshness Assessment
The project requires the latest valid ISO order date to be no more than one day old.
Current Result
- 📅 Latest valid ISO order date: 18 January 2026
- 📆 Assessment date: 5 October 2026
- ⏳ Data age: 260 days
- ❌ Freshness status: FAIL
This indicates that the supplied data is significantly older than the defined daily reporting requirement.
🧮 9. KPI Eligibility
For KPI calculations, the analysis applies strict eligibility rules. A record must have valid:
- 🆔 Order ID
- 📅 ISO order date
- 🔢 Positive whole-number quantity
- 💰 Non-negative unit price
- 🏷️ Discount between 0% and 100%
- 💳 Approved payment status
Exact duplicate rows are removed only for the temporary KPI calculation; the original source is not silently altered.
📊 Eligibility Summary
Metric	Value
Raw Records	12
KPI-Eligible Records	5
Excluded Records	7
Eligible Order IDs	RT-1001, RT-1004, RT-1005, RT-1009, RT-1010


💰 10. KPI Snapshot
KPI	Formula	Result
🧾 Total Orders	COUNT(DISTINCT order_id)	5
💵 Gross Sales	SUM(quantity × unit_price)	₹8,791.00
🏷️ Discount Amount	SUM(gross_sales × discount_pct / 100)	₹729.35
💰 Recognized Net Sales	SUM(net_sales) for Paid orders	₹4,514.35
📦 Units Sold	SUM(quantity)	9
🛒 Average Order Value	Recognized Net Sales ÷ Paid Orders	₹1,504.78
💳 Paid Order Rate	Paid Orders ÷ Total Orders × 100	60.00%
↩️ Refund Rate	Refunded Orders ÷ Total Orders × 100	20.00%
❌ Failed Payment Rate	Failed Orders ÷ Total Orders × 100	20.00%
⏳ Pending Payment Rate	Pending Orders ÷ Total Orders × 100	0.00%


📈 11. Business Interpretation
💵 Sales Performance
The KPI-eligible records generated ₹8,791 in gross sales. After discounts, recognized net sales from paid orders amounted to ₹4,514.35.
🛒 Order Value
The calculated Average Order Value is ₹1,504.78, based specifically on recognized net sales divided by paid orders.
💳 Payment Health
The payment mix shows:
- ✅ 60% Paid
- ↩️ 20% Refunded
- ❌ 20% Failed
- ⏳ 0% Pending
The refund and failed-payment rates therefore deserve operational attention, although the small eligible sample size means these figures should be interpreted cautiously.
📦 Units
The dataset contains 9 valid units sold across the KPI-eligible records.
🛠️ 12. Recommended Remediation Plan
1️⃣ Correct Source Data
Resolve invalid and missing dates, quantities, discounts, and city information at the source.
2️⃣ Investigate Duplicate Orders
Review RT-1004 and determine why the same order appears twice.
3️⃣ Enforce Validation Rules
Introduce automated checks for:
- ISO date format 📅
- Positive whole-number quantities 🔢
- Non-negative prices 💰
- Discounts between 0% and 100% 🏷️
- Approved categories and payment statuses ✅
- Unique order IDs 🔐
4️⃣ Improve Data Freshness
Refresh the source data so that the latest valid order date satisfies the ≤1-day freshness requirement.
5️⃣ Block Untrusted KPI Publication
Production KPI reporting should remain blocked while critical quality failures remain unresolved.
6️⃣ Establish Escalation
If an issue remains unresolved after the next refresh:
Data Owner → Analytics Lead → Business / Decision Owner
If an issue could materially mislead a business decision, affected KPIs should be marked “Not Trusted.”
🏁 13. Conclusion
The Retail KPI & Data Quality project demonstrates that accurate KPI reporting depends on reliable source data.
The current dataset provides a useful analytical snapshot, but it does not meet the defined data-quality contract. The most significant concerns are duplicate order IDs, invalid or missing dates, invalid quantities, discount-quality issues, weak core consistency, and severe freshness failure.
The KPI calculations have therefore been restricted to eligible records only, ensuring that invalid transactions do not silently influence the reported metrics.
🎯 Final Assessment
🚨 Overall Data Quality: FAIL — Remediation Required

📊 KPI Snapshot: Auditable, but not production-trusted

Once the source-quality issues are corrected and the freshness requirement is satisfied, the dataset can be reassessed for production KPI reporting.
📚 14. Project Artifacts
This report is supported by the following project artifacts:
- 📓 Retail Data Profile — profiling, missing-value, duplicate, validity, consistency, freshness, and KPI calculations.
- 📄 Retail Data Quality Contract — acceptance thresholds, failure actions, escalation rules, and current assessment.
- 📊 Retail KPI Dictionary — KPI definitions, formulas, business rules, ownership, refresh cadence, quality profile, known issues, and source data dictionary.
✨ Final Takeaway
Clean data → Reliable KPIs → Better decisions. 📊
The project establishes a practical framework for ensuring that retail performance metrics are not only calculated, but also traceable, defensible, and trustworthy.
