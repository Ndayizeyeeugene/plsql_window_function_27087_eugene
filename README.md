🏦 Bank Management System (SQL Project)
 📌 Overview

This project demonstrates a simplified **Bank Management System** using SQL. It is designed for academic purposes to showcase database design, table relationships, JOIN operations, and advanced **window functions** such as `LEAD()` and `NTILE()`.

---
 💼 Business Problem

Banks need a structured way to:

* Store customer information
* Manage multiple bank accounts per customer
* Track financial transactions over time

The challenge is to design a relational database that maintains **data integrity**, supports **efficient querying**, and enables **analytical insights** such as transaction trends and customer segmentation.

---
 🗂️ Database Schema

The system consists of **three related tables**:

 1. Customers

Stores personal details of bank customers.

Primary Key: `customer_id`

 2. Accounts

Stores bank accounts owned by customers.
Primary Key: `account_id`
Foreign Key: `customer_id` → Customers

 3. Transactions

Stores deposits and withdrawals made on accounts.

Primary Key: `transaction_id`
Foreign Key: `account_id` → Accounts


 ER Diagram (Text Description)


Customers (1) ────< Accounts (1) ────< Transactions
```

* One customer can have many accounts
* One account can have many transactions

---

 JOIN Queries

 Customers and their accounts

```sql
SELECT c.full_name, a.account_type, a.balance
FROM Customers c
JOIN Accounts a ON c.customer_id = a.customer_id;
```

 Transactions with customer details

```sql
SELECT c.full_name, a.account_id, t.amount, t.transaction_type
FROM Customers c
JOIN Accounts a ON c.customer_id = a.customer_id
JOIN Transactions t ON a.account_id = t.account_id;
```

 Window Function Queries

 🔹 LEAD(): Compare each transaction with the next one

```sql
SELECT
    account_id,
    transaction_date,
    amount,
    LEAD(amount) OVER (
        PARTITION BY account_id
        ORDER BY transaction_date
    ) AS next_transaction_amount
FROM Transactions;
```

 NTILE(): Group transactions by amount

```sql
SELECT
    transaction_id,
    account_id,
    amount,
    NTILE(3) OVER (ORDER BY amount DESC) AS amount_group
FROM Transactions;
```

---

 Key Insights

* Customers can own multiple accounts, enabling flexible banking services
* Window functions allow transaction comparison without complex JOINs
* `LEAD()` helps analyze changes between consecutive transactions
* `NTILE()` supports transaction segmentation (high, medium, low values)

---

 References

* Silberschatz, A., Korth, H. F., & Sudarshan, S. *Database System Concepts*
* Oracle SQL Documentation – Window Functions
* PostgreSQL Official Documentation

---

 Integrity Statement

I declare that this project is my original work. All SQL queries were written by me for academic purposes. Any external references used were properly acknowledged. This work has not been copied or submitted by another student.

-
