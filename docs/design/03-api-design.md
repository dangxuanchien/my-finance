# API Design

## Overview

This document defines the RESTful API design for the **Personal Finance Tracker** application. It serves as the contract between the Frontend and Backend, ensuring consistency, maintainability, and scalability.

---

# Base URL

```text
/api/v1
```

---

# Authentication

All endpoints (except authentication endpoints such as Login/Register) require a valid JWT access token.

```http
Authorization: Bearer <JWT_TOKEN>
```

---

# Response Format

## Success Response

```json
{
  "success": true,
  "data": {},
  "message": null
}
```

## Error Response

```json
{
  "success": false,
  "errorCode": "TRANSACTION_NOT_FOUND",
  "message": "Transaction not found"
}
```

---

# Transaction APIs

## Get Transactions

**Endpoint**

```http
GET /transactions
```

### Query Parameters

| Parameter  | Type    | Required | Description                               |
| ---------- | ------- | -------- | ----------------------------------------- |
| page       | integer | No       | Page number (default: 1)                  |
| size       | integer | No       | Number of records per page (default: 20)  |
| keyword    | string  | No       | Search by description                     |
| categoryId | UUID    | No       | Filter by category                        |
| accountId  | UUID    | No       | Filter by account                         |
| type       | enum    | No       | INCOME or EXPENSE                         |
| startDate  | date    | No       | Start date (yyyy-MM-dd)                   |
| endDate    | date    | No       | End date (yyyy-MM-dd)                     |
| sort       | string  | No       | Sort field (e.g. transactionDate, amount) |

### Response

```json
{
  "items": [],
  "page": 1,
  "size": 20,
  "totalItems": 320,
  "totalPages": 16
}
```

---

## Get Transaction Detail

**Endpoint**

```http
GET /transactions/{id}
```

### Response

```json
{
  "id": "",
  "amount": 50000,
  "type": "EXPENSE",
  "category": {},
  "account": {},
  "transactionDate": "2026-07-12",
  "description": "Dinner",
  "note": "",
  "attachments": []
}
```

---

## Create Transaction

**Endpoint**

```http
POST /transactions
```

### Request Body

```json
{
  "accountId": "",
  "categoryId": "",
  "amount": 120000,
  "type": "EXPENSE",
  "transactionDate": "2026-07-12",
  "description": "Dinner",
  "note": ""
}
```

### Response

```http
201 Created
```

---

## Update Transaction

**Endpoint**

```http
PUT /transactions/{id}
```

### Request Body

```json
{
  "categoryId": "",
  "amount": 150000,
  "description": "",
  "note": ""
}
```

---

## Delete Transaction

**Endpoint**

```http
DELETE /transactions/{id}
```

---

# Category APIs

## Get Categories

```http
GET /categories
```

### Response

```json
[
  {
    "id": "",
    "name": "Food",
    "type": "EXPENSE",
    "color": "#FFAA00",
    "icon": "food"
  }
]
```

---

## Create Category

```http
POST /categories
```

```json
{
  "name": "Coffee",
  "type": "EXPENSE",
  "color": "#333333",
  "icon": "coffee"
}
```

---

## Update Category

```http
PUT /categories/{id}
```

---

## Delete Category

```http
DELETE /categories/{id}
```

---

# Account APIs

## Get Accounts

```http
GET /accounts
```

### Response

```json
[
  {
    "id": "",
    "name": "MB Bank",
    "type": "BANK",
    "balance": 12000000
  }
]
```

---

## Create Account

```http
POST /accounts
```

```json
{
  "name": "Techcombank",
  "type": "BANK",
  "balance": 1000000
}
```

---

## Update Account

```http
PUT /accounts/{id}
```

---

## Delete Account

```http
DELETE /accounts/{id}
```

---

# Dashboard APIs

All statistical calculations are performed by the Backend. The Frontend is responsible only for rendering the returned data.

## Dashboard Summary

```http
GET /dashboard/summary
```

```json
{
  "totalIncome": 35000000,
  "totalExpense": 18000000,
  "balance": 17000000,
  "transactionCount": 156
}
```

---

## Expense by Category

```http
GET /dashboard/category
```

### Query Parameters

| Parameter | Type |
| --------- | ---- |
| startDate | date |
| endDate   | date |

```json
[
  {
    "categoryId": "",
    "categoryName": "Food",
    "amount": 3500000,
    "percentage": 28.5
  }
]
```

---

## Monthly Trend

```http
GET /dashboard/monthly
```

```json
[
  {
    "month": "2026-01",
    "income": 35000000,
    "expense": 22000000
  }
]
```

---

## Daily Expense Trend

```http
GET /dashboard/daily
```

```json
[
  {
    "date": "2026-07-01",
    "expense": 320000
  }
]
```

---

## Spending Frequency

```http
GET /dashboard/frequency
```

```json
[
  {
    "hour": 8,
    "count": 4
  }
]
```

---

## Top Expense Categories

```http
GET /dashboard/top-category
```

```json
[
  {
    "category": "Food",
    "amount": 5400000
  }
]
```

---

## Cash Flow

```http
GET /dashboard/cashflow
```

```json
[
  {
    "date": "2026-07-01",
    "income": 500000,
    "expense": 250000
  }
]
```

---

# Report APIs

## Export Excel

```http
GET /reports/export/excel
```

### Query Parameters

| Parameter | Type |
| --------- | ---- |
| startDate | date |
| endDate   | date |

**Response**

```
Excel File
```

---

## Export CSV

```http
GET /reports/export/csv
```

---

# User APIs

## Get User Profile

```http
GET /users/me
```

```json
{
  "id": "",
  "name": "",
  "email": ""
}
```

---

## Update User Profile

```http
PUT /users/me
```

---

# Health Check

```http
GET /health
```

```json
{
  "status": "UP"
}
```

---

# Standard Error Codes

| HTTP Status | Error Code            | Description             |
| ----------- | --------------------- | ----------------------- |
| 400         | VALIDATION_ERROR      | Validation failed       |
| 400         | INVALID_REQUEST       | Invalid request         |
| 401         | UNAUTHORIZED          | Authentication required |
| 403         | FORBIDDEN             | Access denied           |
| 404         | TRANSACTION_NOT_FOUND | Transaction not found   |
| 404         | CATEGORY_NOT_FOUND    | Category not found      |
| 404         | ACCOUNT_NOT_FOUND     | Account not found       |
| 409         | DUPLICATE_CATEGORY    | Category already exists |
| 500         | INTERNAL_SERVER_ERROR | Unexpected server error |

---

# API Versioning

```text
/api/v1/...
```

---

# Future Enhancements

* Import transactions from CSV/Excel
* Bank synchronization
* Monthly budget management
* Savings goals
* Recurring transactions
* Push notifications & reminders
* AI-powered spending insights
* Multi-currency support
* Shared finance management
* Transaction tags
* Attachment uploads
* Audit logs

---

# Notes

* All APIs use JSON format.
* Date and time follow the ISO 8601 standard.
* JWT authentication is required for all protected endpoints.
* Dashboard endpoints return aggregated data only.
* Pagination is applied to all list endpoints.
* All endpoints follow RESTful API design principles.
