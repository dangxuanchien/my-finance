# Frontend Design

## Overview

This document describes the frontend architecture, development guidelines, and project structure for the **Personal Finance Tracker** application.

The primary goals of this design are:

* Maintainable architecture
* Feature-based organization
* Scalable project structure
* Consistent coding standards
* Clear separation of concerns
* High performance and excellent developer experience

---

# Technology Stack

| Category      | Technology           |
| ------------- | -------------------- |
| Framework     | Next.js              |
| Language      | TypeScript           |
| UI Library    | Material UI          |
| Data Fetching | TanStack Query       |
| HTTP Client   | Axios                |
| Database      | PostgreSQL (Backend) |
| Backend API   | NestJS               |
| ORM           | Prisma ORM           |

---

# Application Architecture

The frontend follows a **Feature-Based Architecture**, where each business feature is isolated into its own module.

Benefits:

* Easier maintenance
* Better scalability
* Clear ownership
* High reusability
* Reduced coupling

Application Flow:

```text
Page
    ↓
Feature
    ↓
Hook
    ↓
API Service
    ↓
NestJS API
```

---

# Project Structure

```text
src/
│
├── app/
├── components/
│
├── features/
│   ├── auth/
│   ├── dashboard/
│   ├── transaction/
│   ├── account/
│   └── category/
│
├── hooks/
├── lib/
├── providers/
├── services/
├── styles/
├── types/
├── utils/
├── constants/
└── middleware.ts
```

---

# Directory Responsibilities

| Directory  | Responsibility                |
| ---------- | ----------------------------- |
| app        | Next.js App Router            |
| components | Shared reusable UI components |
| features   | Business modules              |
| hooks      | Shared custom hooks           |
| services   | Shared API services           |
| providers  | React Providers               |
| styles     | Global styles                 |
| utils      | Utility functions             |
| constants  | Global constants              |
| lib        | Shared library configuration  |

---

# Routing Strategy

The application uses **Next.js App Router**.

```text
app/
│
├── login/
├── dashboard/
├── transactions/
├── accounts/
├── categories/
├── settings/
└── reports/
```

Protected routes require authentication.

---

# Layout Structure

```text
RootLayout
    │
    ├── Header
    ├── Sidebar
    ├── Main Content
    └── Footer
```

Each page is rendered inside the Root Layout.

---

# State Management

The application separates **Server State** from **Client State**.

## Server State

Managed by **TanStack Query**

Examples:

* Transactions
* Categories
* Accounts
* Dashboard
* Reports

---

## Client State

Managed using React built-in hooks.

Examples:

* Dialog visibility
* Selected tab
* Drawer state
* Filter state
* Form state

---

## Global Context

React Context is used for:

* Authentication
* Theme
* User preferences

---

# Data Fetching Strategy

All server communication must go through the API layer.

```text
Page
    ↓
Feature Hook
    ↓
API Service
    ↓
Axios Client
    ↓
NestJS API
```

Components should never call Axios directly.

---

# API Layer

API communication is organized by feature.

Example:

```text
features/
    transaction/
        api/
            transaction.service.ts
```

Responsibilities:

* API requests
* Response mapping
* Error handling
* Type safety

---

# Authentication

Authentication flow:

```text
Login
    ↓
JWT Authentication
    ↓
Store Access Token
    ↓
Protected Routes
    ↓
API Requests
```

Authentication responsibilities:

* Login
* Logout
* Route protection
* Token expiration handling
* Automatic redirect

---

# UI Component Architecture

Shared components are located inside:

```text
components/
```

Examples:

* Button
* Input
* Select
* Dialog
* Table
* Pagination
* Loading
* Empty State
* Confirm Dialog

Business-specific components belong to their corresponding feature.

Example:

```text
features/
    transaction/
        components/
            TransactionTable.tsx
            TransactionForm.tsx
```

---

# Form Handling

Forms should:

* Use controlled components
* Perform client-side validation
* Display validation errors
* Submit through the API layer

---

# Error Handling

Common HTTP errors:

| Status | Action                             |
| ------ | ---------------------------------- |
| 400    | Show validation errors             |
| 401    | Redirect to Login                  |
| 403    | Show permission denied message     |
| 404    | Show not found page                |
| 500    | Show unexpected error notification |

---

# Theme

Material UI Theme is responsible for:

* Color palette
* Typography
* Spacing
* Breakpoints
* Component customization

Support:

* Light Theme
* Dark Theme

---

# Performance Optimization

Recommended techniques:

* Code Splitting
* Lazy Loading
* Dynamic Imports
* Memoization
* Query Caching
* Pagination
* Debounced Search
* Image Optimization

---

# Coding Convention

General principles:

* Use TypeScript strict mode.
* Prefer functional components.
* Keep components focused on a single responsibility.
* Avoid duplicated business logic.
* Extract reusable logic into custom hooks.
* Use descriptive naming conventions.
* Keep components small and reusable.

---

# Folder Convention

Each feature should follow a consistent structure.

Example:

```text
transaction/
│
├── api/
├── components/
├── hooks/
├── types/
├── constants/
├── utils/
└── index.ts
```

Each feature should be self-contained and avoid unnecessary dependencies on other features.

---

# Future Improvements

Potential future enhancements:

* Offline mode
* Progressive Web App (PWA)
* Real-time notifications
* Multi-language support
* Accessibility improvements
* Advanced dashboard visualizations

---

# Development Principles

* Feature-first organization
* Reusable components
* Separation of concerns
* Type safety
* API-driven development
* Responsive design
* Accessibility-first
* Performance-oriented implementation

---

# Summary

The frontend architecture is designed around a **Feature-Based Architecture** using **Next.js**, **TypeScript**, **Material UI**, and **TanStack Query**. The project emphasizes modularity, maintainability, scalability, and a clean separation between presentation, business logic, and data access layers.
