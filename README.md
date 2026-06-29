# 📊 PhonePe Analytics Dashboard — Power BI

> An end-to-end data visualization project built on PhonePe transaction data, covering Money Transfers, Loans, Insurance, and Recharge & Bills across **300,000 transactions**.

---

## 🖼️ Dashboard Preview

![image alt](https://github.com/AryanInsights/PhonePe-Analysis-Dashboard/blob/436daeabb50e5e1ea6a8b332653a734fe34fdc88/Snapshot%20of%20PhonePe%20Dashboard.png)

---

## 📌 Project Overview

This Power BI dashboard provides a comprehensive analytical view of PhonePe's platform activity. It tracks key financial metrics, user behavior, transaction success rates, and month-over-month trends — all in an interactive, filterable interface.

| Metric | Value |
|---|---|
| 📦 Total Transactions | 3,00,000 |
| ✅ Successful | 2,87,993 |
| ❌ Failed | 9,980 |
| ⏳ Pending | 2,027 |
| 💰 Total Transaction Value | ₹3,47,43,21,934+ |

---

## 🗂️ Data Model

The semantic model is built on **3 core tables** connected through a Date Table:

### 📋 Tables

#### `All_Transactions`
| Column | Type | Description |
|---|---|---|
| Transaction_ID | Text | Unique transaction identifier (MTX_, RCG_, LON_, INS_) |
| Amount | Decimal | Transaction amount in ₹ |
| User_ID | Text | PhonePe user identifier |
| Service | Text | Service category |
| Service Type | Text | Sub-category of the service |
| Payment_Status | Text | Successful / Failed / Pending |
| Reason | Text | Reason for failure or success |
| Date | Date | Transaction date |

#### `All_Users`
| Column | Type | Description |
|---|---|---|
| User_ID | Text | Unique user identifier |
| Name | Text | User name |
| Age | Whole Number | User age |
| Join_Date | Date | Account creation date |
| Age Segment | Text | Age group classification |

#### `Date_Table`
Custom date table with Year, Month, Quarter, MonthNo, and Day columns for time intelligence.

---

## 📈 Services Analyzed

| Service | Transactions | Total Value |
|---|---|---|
| 💸 Money Transfer | 1,50,000 | ₹37.8 Cr |
| 🏦 Loans | 50,000 | ₹253.3 Cr |
| 🛡️ Insurance | 50,000 | ₹51.3 Cr |
| 📱 Recharge & Bills | 50,000 | ₹5.1 Cr |

### Money Transfer Sub-types
- To UPI ID
- To Mobile Number
- To Self Account
- To QR Code

### Loan Sub-types
- Bike Loan · Gold Loan · Credit Score · Mutual Fund

### Insurance Sub-types
- Health · Car · Bike · Term Life

### Recharge & Bill Sub-types
- Mobile Recharge · DTH · Cable TV · FASTag Recharge

---

## 🧮 DAX Measures

All measures live in the `Measures (2)` table:

```dax
-- Total transaction amount
Total Transaction Value = SUM(All_Transactions[Amount])

-- Count of all transactions
Total Transaction = COUNT(All_Transactions[Transaction_ID])

-- Count of successful transactions only
Successful Transaction =
    CALCULATE([Total Transaction], All_Transactions[Payment_Status] = "Successful")

-- Success rate percentage
Success Rate = DIVIDE([Successful Transaction], [Total Transaction])

-- Distinct active users
Total User = DISTINCTCOUNT(All_Users[User_ID])

-- Previous month transaction value (time intelligence)
Trans Value Prev Mon =
    CALCULATE([Total Transaction Value], DATEADD(Date_Table[Date], -1, MONTH))

-- Month-over-month % change in value
Trans Value MOM% =
    DIVIDE([Total Transaction Value] - [Trans Value Prev Mon], [Trans Value Prev Mon], 0)

-- Previous month transaction count
Total Trans PM =
    CALCULATE([Total Transaction], DATEADD(Date_Table[Date], -1, MONTH))

-- Month-over-month % change in count
Total Trans MOM% =
    DIVIDE([Total Transaction] - [Total Trans PM], [Total Trans PM], 0)
```

---

## 🛠️ Tools & Technologies

| Tool | Usage |
|---|---|
| **Power BI Desktop** | Dashboard development & visualization |
| **DAX** | Custom measures & time intelligence |
| **Power Query (M)** | Data transformation & cleaning |
| **Microsoft Excel / CSV** | Source data |
| **Figma** | Background creation |

---

## 📊 Key Insights (from the Data)

- 🏆 **Money Transfer** is the most-used service with **1.5 lakh transactions**
- 💰 **Loans** drive the highest monetary value at **₹253 Cr+**
- ✅ Overall **Success Rate** is **~96%** across all services
- ⚠️ Most common failure reasons: Wrong PIN, Insufficient Amount, Server Error
- 📅 **Time Intelligence** allows month-over-month trend tracking for both count and value

---

## 📄 License

This project is for educational and portfolio purposes only.
Data used is synthetic/sample data and does not represent real PhonePe user information.

---

⭐ **If you found this project helpful, give it a star!**
