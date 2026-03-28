#  Customer Complaint Tracker — MySQL

![MySQL](https://img.shields.io/badge/Tool-MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-28a745?style=for-the-badge)


##  Project Overview

This project builds a **Customer Complaint Tracking System** using MySQL. It simulates a real-world complaint management workflow for a company that sells biometric hardware — Face Readers and Fingerprint Scanners.

The project demonstrates how MySQL can be used to register, query, and analyse complaint data — generating insights on complaint volume, resolution rates, and product-wise issue breakdown.


##  Business Problem

A biometric hardware company receives 50–100 customer complaints every month. Without a structured system:
- Complaints get lost or delayed
- No visibility into which product has the most issues
- No way to measure resolution performance over time

This project solves that using structured MySQL queries.


##  Files in This Project

| File | Description |
|------|-------------|
| `complaints_analysis.sql` | Full MySQL file — database setup, 30 sample records, 12 analysis queries |
| `README.md` | Project documentation |

---

##  Tools Used

| Tool | Details |
|------|---------|
| MySQL | Version 8.0+ |
| MySQL Workbench | For running queries locally |

---

##  Database Schema

```sql
CREATE DATABASE IF NOT EXISTS complaint_db;
USE complaint_db;

CREATE TABLE complaints (
    complaint_id    INT           PRIMARY KEY AUTO_INCREMENT,
    customer_name   VARCHAR(100)  NOT NULL,
    product         VARCHAR(100)  NOT NULL,   
    issue_type      VARCHAR(100)  NOT NULL,   
    status          VARCHAR(50)   NOT NULL,   
    registered_date DATE          NOT NULL,
    resolved_date   DATE          NULL       
);
```

---

##  Sample Data — All 30 Records

| ID | Customer Name | Product | Issue Type | Status | Registered | Resolved |
|----|--------------|---------|-----------|--------|-----------|---------|
| 1 | Raj Kumar | Face Reader | Connectivity | Resolved | 2025-01-03 | 2025-01-06 |
| 2 | Priya Singh | Fingerprint Scanner | Software | Resolved | 2025-01-05 | 2025-01-07 |
| 3 | Amit Sharma | Face Reader | Hardware | Pending | 2025-01-07 | — |
| 4 | Sunita Verma | Face Reader | Connectivity | Resolved | 2025-01-10 | 2025-01-12 |
| 5 | Deepak Yadav | Fingerprint Scanner | Hardware | In Progress | 2025-01-12 | — |
| 6 | Meena Joshi | Face Reader | Software | Resolved | 2025-01-14 | 2025-01-17 |
| 7 | Rahul Gupta | Fingerprint Scanner | Connectivity | Resolved | 2025-01-15 | 2025-01-18 |
| 8 | Kavita Patel | Face Reader | Hardware | Pending | 2025-01-18 | — |
| 9 | Nitin Mishra | Face Reader | Software | Resolved | 2025-01-20 | 2025-01-22 |
| 10 | Ankita Singh | Fingerprint Scanner | Hardware | Resolved | 2025-01-22 | 2025-01-25 |
| 11 | Vikram Tiwari | Face Reader | Connectivity | Resolved | 2025-02-01 | 2025-02-04 |
| 12 | Pooja Agarwal | Face Reader | Software | In Progress | 2025-02-03 | — |
| 13 | Sanjay Dubey | Fingerprint Scanner | Hardware | Resolved | 2025-02-05 | 2025-02-08 |
| 14 | Rekha Chauhan | Face Reader | Connectivity | Pending | 2025-02-07 | — |
| 15 | Manoj Kumar | Fingerprint Scanner | Software | Resolved | 2025-02-10 | 2025-02-12 |
| 16 | Geeta Yadav | Face Reader | Hardware | Resolved | 2025-02-12 | 2025-02-15 |
| 17 | Suresh Pandey | Fingerprint Scanner | Connectivity | Resolved | 2025-02-14 | 2025-02-16 |
| 18 | Nisha Sharma | Face Reader | Software | Pending | 2025-02-18 | — |
| 19 | Arun Srivastava | Fingerprint Scanner | Hardware | Resolved | 2025-02-20 | 2025-02-23 |
| 20 | Lakshmi Devi | Face Reader | Connectivity | Resolved | 2025-02-22 | 2025-02-25 |
| 21 | Rohit Bajpai | Face Reader | Hardware | Resolved | 2025-03-02 | 2025-03-05 |
| 22 | Shweta Nair | Fingerprint Scanner | Connectivity | In Progress | 2025-03-04 | — |
| 23 | Dinesh Gupta | Face Reader | Software | Resolved | 2025-03-06 | 2025-03-08 |
| 24 | Preeti Jain | Face Reader | Connectivity | Pending | 2025-03-09 | — |
| 25 | Harish Awasthi | Fingerprint Scanner | Hardware | Resolved | 2025-03-11 | 2025-03-14 |
| 26 | Usha Tripathi | Face Reader | Software | Resolved | 2025-03-13 | 2025-03-15 |
| 27 | Pankaj Rao | Fingerprint Scanner | Connectivity | Resolved | 2025-03-16 | 2025-03-18 |
| 28 | Seema Kulkarni | Face Reader | Hardware | Pending | 2025-03-19 | — |
| 29 | Ajay Mehta | Face Reader | Software | Resolved | 2025-03-21 | 2025-03-23 |
| 30 | Divya Kapoor | Fingerprint Scanner | Hardware | Resolved | 2025-03-24 | 2025-03-26 |

---

##  Queries & Results

### Q1 — Total Complaints

```sql
SELECT COUNT(*) AS total_complaints FROM complaints;
```
| total_complaints |
|-----------------|
| 30 |

---

### Q2 — Complaints by Product

```sql
SELECT product, COUNT(*) AS total_complaints
FROM complaints
GROUP BY product
ORDER BY total_complaints DESC;
```
| product | total_complaints |
|---------|-----------------|
| Face Reader | 19 |
| Fingerprint Scanner | 11 |

---

### Q3 — Complaints by Issue Type

```sql
SELECT issue_type, COUNT(*) AS total_complaints
FROM complaints
GROUP BY issue_type
ORDER BY total_complaints DESC;
```
| issue_type | total_complaints |
|-----------|-----------------|
| Hardware | 11 |
| Software | 10 |
| Connectivity | 9 |

---

### Q4 — Complaints by Status

```sql
SELECT status, COUNT(*) AS total
FROM complaints
GROUP BY status
ORDER BY total DESC;
```
| status | total |
|--------|-------|
| Resolved | 21 |
| Pending | 6 |
| In Progress | 3 |

---

### Q5 — Resolution Rate (%)

```sql
SELECT
    ROUND(
        100.0 * SUM(CASE WHEN status = 'Resolved' THEN 1 ELSE 0 END) / COUNT(*),
    2) AS resolution_rate_percent
FROM complaints;
```
| resolution_rate_percent |
|------------------------|
| 70.00 |

---

### Q6 — Average Resolution Time (Days)

```sql
SELECT ROUND(AVG(DATEDIFF(resolved_date, registered_date)), 2) AS avg_resolution_days
FROM complaints
WHERE status = 'Resolved' AND resolved_date IS NOT NULL;
```
| avg_resolution_days |
|--------------------|
| 2.90 |

---

### Q7 — Monthly Complaint Volume

```sql
SELECT DATE_FORMAT(registered_date, '%Y-%m') AS month, COUNT(*) AS total_complaints
FROM complaints
GROUP BY month
ORDER BY month ASC;
```
| month | total_complaints |
|-------|-----------------|
| 2025-01 | 10 |
| 2025-02 | 10 |
| 2025-03 | 10 |

---

### Q8 — All Pending Complaints (Oldest First)

```sql
SELECT complaint_id, customer_name, product, issue_type, registered_date
FROM complaints
WHERE status = 'Pending'
ORDER BY registered_date ASC;
```
| ID | Customer | Product | Issue | Registered |
|----|---------|---------|-------|-----------|
| 3 | Amit Sharma | Face Reader | Hardware | 2025-01-07 |
| 8 | Kavita Patel | Face Reader | Hardware | 2025-01-18 |
| 14 | Rekha Chauhan | Face Reader | Connectivity | 2025-02-07 |
| 18 | Nisha Sharma | Face Reader | Software | 2025-02-18 |
| 24 | Preeti Jain | Face Reader | Connectivity | 2025-03-09 |
| 28 | Seema Kulkarni | Face Reader | Hardware | 2025-03-19 |

---

### Q9 — Product + Issue Type Breakdown

```sql
SELECT product, issue_type, COUNT(*) AS total
FROM complaints
GROUP BY product, issue_type
ORDER BY product, total DESC;
```
| product | issue_type | total |
|---------|-----------|-------|
| Face Reader | Connectivity | 7 |
| Face Reader | Hardware | 6 |
| Face Reader | Software | 6 |
| Fingerprint Scanner | Hardware | 5 |
| Fingerprint Scanner | Connectivity | 4 |
| Fingerprint Scanner | Software | 2 |

---

### Q10 — Top 5 Fastest Resolved Complaints

```sql
SELECT complaint_id, customer_name, product, issue_type,
       registered_date, resolved_date,
       DATEDIFF(resolved_date, registered_date) AS days_to_resolve
FROM complaints
WHERE status = 'Resolved'
ORDER BY days_to_resolve ASC
LIMIT 5;
```
| ID | Customer | Product | Issue | Registered | Resolved | Days |
|----|---------|---------|-------|-----------|---------|------|
| 2 | Priya Singh | Fingerprint Scanner | Software | 2025-01-05 | 2025-01-07 | 2 |
| 4 | Sunita Verma | Face Reader | Connectivity | 2025-01-10 | 2025-01-12 | 2 |
| 23 | Dinesh Gupta | Face Reader | Software | 2025-03-06 | 2025-03-08 | 2 |
| 26 | Usha Tripathi | Face Reader | Software | 2025-03-13 | 2025-03-15 | 2 |
| 27 | Pankaj Rao | Fingerprint Scanner | Connectivity | 2025-03-16 | 2025-03-18 | 2 |

---

### Q11 — Monthly Volume by Product

```sql
SELECT DATE_FORMAT(registered_date, '%Y-%m') AS month, product, COUNT(*) AS total_complaints
FROM complaints
GROUP BY month, product
ORDER BY month, product;
```
| month | product | total |
|-------|---------|-------|
| 2025-01 | Face Reader | 6 |
| 2025-01 | Fingerprint Scanner | 4 |
| 2025-02 | Face Reader | 6 |
| 2025-02 | Fingerprint Scanner | 4 |
| 2025-03 | Face Reader | 7 |
| 2025-03 | Fingerprint Scanner | 3 |

---

### Q12 — Complaints Open More Than 30 Days

```sql
SELECT complaint_id, customer_name, product, issue_type, status,
       registered_date,
       DATEDIFF(CURDATE(), registered_date) AS days_open
FROM complaints
WHERE status IN ('Pending', 'In Progress')
  AND DATEDIFF(CURDATE(), registered_date) > 30
ORDER BY days_open DESC;
```
> Result depends on today's date. Any complaint registered before today minus 30 days will appear here.

---

##  Key Insights

- Total complaints: **30**
- Most complained product: **Face Reader (63%)**
- Most common issue: **Hardware (37%)**
- Resolution rate: **70%**
- Average resolution time: **2.9 days**
- All 6 pending complaints belong to: **Face Reader product**
- Monthly trend: **Stable at 10 complaints per month**

---

##  What I Learned

- Designing a MySQL database schema from scratch
- Writing analytical queries using `GROUP BY`, `COUNT`, `AVG`, `DATEDIFF`
- Using `DATE_FORMAT` for monthly trend analysis
- Using `CASE WHEN` inside `SUM` for percentage calculations
- Using `LIMIT` for top-N analysis
- Translating real business problems into structured SQL queries

---

##  Author

**Chandan Mourya**
 Aspiring Data Analyst | MBA Candidate — Amity University
 
🔗 [LinkedIn](https://www.linkedin.com/in/chandan-mourya-070a93216)
