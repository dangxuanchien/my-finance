# Sprint Planning

## Sprint 01 - Project Foundation

**Goal**

Setup project foundation and development environment.

**Estimate:** 5 Days

### Documentation

- [ ] Project Overview
- [ ] Requirements
- [ ] Roadmap
- [ ] ERD
- [ ] API Design

### Backend

- [ ] Initialize NestJS
- [ ] Setup Prisma
- [ ] Setup PostgreSQL
- [ ] Setup Swagger
- [ ] Health Check API

### Frontend

- [ ] Initialize Next.js
- [ ] Install MUI
- [ ] Setup TanStack Query
- [ ] Setup Axios
- [ ] Create Layout

### DevOps

- [ ] Docker Compose
- [ ] PostgreSQL Container
- [ ] Environment Configuration

**Done Criteria**

- Backend running
- Frontend running
- PostgreSQL connected
- Swagger available

---

## Sprint 02 - Authentication & User Management

**Goal**

Build authentication module.

**Estimate:** 5 Days

### Database

- [ ] User Table

### Backend

- [ ] Register API
- [ ] Login API
- [ ] JWT Authentication
- [ ] Refresh Token
- [ ] Password Hash

### Frontend

- [ ] Login Page
- [ ] Register Page
- [ ] Protected Routes
- [ ] Logout

### Testing

- [ ] Register
- [ ] Login
- [ ] Authorization

**Done Criteria**

User can login successfully.

---

## Sprint 03 - Database & Excel Import

**Goal**

Import Vietcombank statements into database.

**Estimate:** 7 Days

### Database

- [ ] Accounts Table
- [ ] Categories Table
- [ ] Transactions Table
- [ ] Import Batches Table

### Backend

- [ ] Upload API
- [ ] Read Excel
- [ ] Validate File
- [ ] Parse Vietcombank
- [ ] Normalize Data
- [ ] Save Transactions
- [ ] Save Import Batch
- [ ] Duplicate Detection

### Frontend

- [ ] Upload Page
- [ ] Upload Component
- [ ] Import Result

### Testing

- [ ] Import Success
- [ ] Invalid File
- [ ] Duplicate File

**Done Criteria**

User can import Excel successfully.

---

## Sprint 04 - Transaction Management

**Goal**

Manage imported transactions.

**Estimate:** 6 Days

### Backend

- [ ] Transaction CRUD
- [ ] Search API
- [ ] Filter API
- [ ] Pagination
- [ ] Update Category
- [ ] Delete Transaction

### Frontend

- [ ] Transaction List
- [ ] Search
- [ ] Filter
- [ ] Pagination
- [ ] Transaction Detail
- [ ] Edit Transaction

### Testing

- [ ] CRUD
- [ ] Search
- [ ] Filter

**Done Criteria**

Users can manage all transactions.

---

## Sprint 05 - Dashboard (MVP Release)

**Goal**

Build dashboard and financial overview.

**Estimate:** 6 Days

### Backend

- [ ] Summary API
- [ ] Monthly Statistics
- [ ] Category Statistics
- [ ] Income vs Expense

### Frontend

- [ ] Summary Cards
- [ ] Monthly Chart
- [ ] Category Chart
- [ ] Cash Flow Chart

### Testing

- [ ] Dashboard Data
- [ ] Charts

**Done Criteria**

🎉 MVP Completed

---

## Sprint 06 - Category & Rule Engine

**Goal**

Automatically categorize transactions.

**Estimate:** 5 Days

### Backend

- [ ] Category CRUD
- [ ] Rule CRUD
- [ ] Auto Categorization

### Frontend

- [ ] Category Management
- [ ] Rule Management

### Testing

- [ ] Rule Matching
- [ ] Auto Category

**Done Criteria**

Transactions can be categorized automatically.

---

## Sprint 07 - Budget & Reports

**Goal**

Budget planning and reporting.

**Estimate:** 5 Days

### Backend

- [ ] Budget API
- [ ] Monthly Report
- [ ] Yearly Report

### Frontend

- [ ] Budget Page
- [ ] Report Page
- [ ] Budget Progress

### Testing

- [ ] Budget Calculation
- [ ] Reports

**Done Criteria**

Users can manage budgets and reports.

---

## Sprint 08 - AI Insights

**Goal**

Provide intelligent financial insights.

**Estimate:** 7 Days

### Backend

- [ ] AI Analysis
- [ ] Spending Summary
- [ ] Expense Prediction

### Frontend

- [ ] AI Insight Page
- [ ] Recommendation Cards

### Testing

- [ ] AI Response

**Done Criteria**

Users receive AI-powered insights.

---

## Sprint 09 - Multi-Bank Support

**Goal**

Support multiple banks.

**Estimate:** 7 Days

### Backend

- [ ] MB Bank Parser
- [ ] Techcombank Parser
- [ ] ACB Parser

### Frontend

- [ ] Account Management
- [ ] Multi Bank Import

### Testing

- [ ] Import Multiple Banks

**Done Criteria**

Support importing statements from multiple banks.

---

## Sprint 10 - Deployment & Optimization

**Goal**

Prepare the application for production.

**Estimate:** 5 Days

### Backend

- [ ] Performance Optimization
- [ ] Logging
- [ ] Exception Handling

### Frontend

- [ ] Performance Optimization
- [ ] Responsive UI
- [ ] Loading Skeleton

### DevOps

- [ ] Docker
- [ ] CI/CD
- [ ] Production Environment

### Testing

- [ ] End-to-End Testing
- [ ] Production Testing

**Done Criteria**

🚀 Production Ready