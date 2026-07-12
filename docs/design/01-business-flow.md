# Business Flow

## Overview

Finance Hub helps users import bank statements, organize transactions, categorize expenses, and analyze personal finances.

---

# Actors

## User

The main user of the system.

Capabilities:

- Register
- Login
- Import bank statement
- Manage transactions
- Manage categories
- View dashboard
- Configure settings

---

# Modules

- Authentication
- User
- Bank Account
- Import
- Transaction
- Category
- Dashboard
- Reports

---

# Main Business Flow

```text
Login
    │
    ▼
Dashboard
    │
    ▼
Import Bank Statement
    │
    ▼
Validate File
    │
    ▼
Parse Excel
    │
    ▼
Normalize Data
    │
    ▼
Save Transactions
    │
    ▼
Auto Categorize
    │
    ▼
Transaction List
    │
    ▼
Dashboard
    │
    ▼
Reports
```

---

# Business Flow Details

## Authentication

User logs into the system.

↓

JWT Token generated.

↓

User accesses application.

---

## Import Statement

User uploads an Excel statement.

↓

System validates the file.

↓

Parser extracts transaction data.

↓

Normalize all transactions.

↓

Save Import Batch.

↓

Save Transactions.

↓

Generate Import Summary.

---

## Transaction Management

User can

- Search
- Filter
- Edit
- Delete
- Assign Category

---

## Dashboard

Dashboard displays

- Total Income
- Total Expense
- Current Balance
- Monthly Spending
- Top Categories

---

# Business Rules

## BR-001

One user can own multiple bank accounts.

---

## BR-002

One bank account contains many transactions.

---

## BR-003

One import batch creates many transactions.

---

## BR-004

One transaction belongs to only one category.

---

## BR-005

Transactions should not be duplicated.

Duplicate Condition

Account

+

Transaction Date

+

Amount

+

Description

---

## BR-006

Deleting a transaction performs Soft Delete.

---

## BR-007

Imported transactions are immutable.

Original bank data must always be preserved.

Users can only edit metadata such as

- Category
- Note
- Tag

---

## BR-008

Categories can be

- System Category
- User Category

---

## MVP Scope

Included

- Login
- Import Excel
- Transactions
- Categories
- Dashboard

Excluded

- AI
- Budget
- Mobile
- Notification
- Multi-bank

---

## Future Scope

- AI Insights
- Budget Planning
- Multi-bank
- Notification
- Mobile Application
- Investment Tracking