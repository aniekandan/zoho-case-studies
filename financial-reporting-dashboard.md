## 🏦 Business Context
The organization required a unified, real-time financial reporting system to replace manual spreadsheet-based analysis. The goal was to provide executives with instant visibility into Profit & Loss (P&L) and Balance Sheets while automating the accounting lifecycle of company assets.

## 🛠️ The Technical Architecture
I architected a multi-app synchronization pipeline leveraging the Zoho Finance Suite and custom middleware logic:

*   **Zoho Analytics (SQL Engine):** Acted as the core reporting layer. I built complex SQL query tables to wrangle raw accrual transactions from Zoho Books into structured monthly Actuals, Cumulative Profits, and Budget comparisons [1-3].
*   **Zoho Creator (Asset Hub):** Developed a custom Asset Management module to track the lifecycle of company property, which served as the source of truth for asset disposal events [4, 5].
*   **Zoho Books (Accounting):** Utilized as the transactional database and the destination for automated journal entries [6, 7].
*   **Deluge & REST APIs:** Custom scripts managed the flow of data, ensuring that when an asset was marked as "Sold" in Creator, a draft Journal Entry was automatically generated in Books for manual review and publishing [8, 9].

## 🧩 Key Challenges & Solutions

### 1. Complex SQL Data Wrangling
**Challenge:** Standard reports couldn't show Actuals, Cumulative totals, and Budgets in a single view with previous-year comparisons.
**Solution:** I implemented a layered SQL architecture. I created separate queries for Actual Profits, Cumulative Profits, and Budgets, then unified them using **Inner JOIN** operations and **Self-Joins** to achieve the "Previous Year" data comparison within the same row [1, 3, 10].

### 2. Chart of Account Inconsistency
**Challenge:** The client's reporting categories (e.g., General and Admin Expenses) were artificial "sum-of" categories not represented as single accounts in Zoho Books [3, 11].
**Solution:** I modified the SQL logic to dynamically aggregate these artificial categories based on a custom mapping table, ensuring the final dashboard matched the client's preferred Excel-based formatting [3, 12].

### 3. Automated Asset Disposal
**Challenge:** Manually creating journal entries for asset sales was prone to human error and delayed financial closing.
**Solution:** Built a custom function in Zoho Books to pull FA (Fixed Asset) and FA Disposal accounts into Zoho Creator [4]. A workflow was then triggered on disposal, calculating the net book value and pushing the draft journal directly into the ledger [8].

## 📈 Business Impact
*   **Real-Time Visibility:** Integrated all Summary and Detailed P&L reports into a single interactive page for instant executive review [12, 13].
*   **Improved Accuracy:** Eliminated data entry errors in asset disposal by automating the journal generation process [8].
*   **Metric Automation:** Automated the calculation of key metrics including **Gross Profit**, **Profit Before Tax**, and **Profit After Tax (at 32%)** with built-in variance analysis [13, 14].

---
*Technical Stack: Zoho Analytics, SQL (Zoho Analytics), Zoho Books, Zoho Creator, Deluge (Scripting).*
