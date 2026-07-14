# Backend Design

## Overview

This document describes the backend architecture, project structure, development principles, and technical guidelines for the **Personal Finance Tracker** application.

The backend is designed using **NestJS Modular Architecture** with a focus on:

* Maintainability
* Scalability
* Separation of concerns
* Type safety
* Clean business logic organization
* Easy integration with frontend applications

---

# Technology Stack

| Category          | Technology        |
| ----------------- | ----------------- |
| Framework         | NestJS            |
| Language          | TypeScript        |
| ORM               | Prisma ORM        |
| Database          | PostgreSQL        |
| Authentication    | JWT               |
| API Documentation | Swagger / OpenAPI |
| Validation        | class-validator   |
| Configuration     | @nestjs/config    |
| Testing           | Jest              |

---

# Backend Architecture

The backend follows a **Modular Layered Architecture**.

High-level request flow:

```text
Client

↓

Controller

↓

Service

↓

Prisma ORM

↓

PostgreSQL Database
```

---

# Architecture Principles

The backend follows these principles:

## Separation of Concerns

Each layer has a specific responsibility.

* Controller handles HTTP communication.
* Service handles business logic.
* Prisma handles database access.
* DTO handles data validation and transformation.

---

## Dependency Injection

NestJS dependency injection is used for:

* Services
* Database connection
* Configuration
* External dependencies

Benefits:

* Easier testing
* Better maintainability
* Loose coupling

---

# Project Structure

```text
src/

├── app.module.ts
├── main.ts
│
├── auth/
│   ├── auth.controller.ts
│   ├── auth.service.ts
│   ├── auth.module.ts
│   ├── dto/
│   ├── guards/
│   └── strategies/
│
├── users/
│   ├── users.controller.ts
│   ├── users.service.ts
│   ├── users.module.ts
│   └── dto/
│
├── transactions/
│   ├── transactions.controller.ts
│   ├── transactions.service.ts
│   ├── transactions.module.ts
│   ├── dto/
│   └── types/
│
├── accounts/
│
├── categories/
│
├── dashboard/
│
├── reports/
│
├── prisma/
│   ├── prisma.module.ts
│   └── prisma.service.ts
│
├── common/
│   ├── filters/
│   ├── interceptors/
│   ├── decorators/
│   ├── guards/
│   └── exceptions/
│
└── config/
    └── configuration.ts
```

---

# Module Design

The backend is organized by business domain.

Main modules:

```text
Auth Module

User Module

Transaction Module

Account Module

Category Module

Dashboard Module

Report Module
```

Each module owns:

* Controller
* Service
* DTO
* Business logic
* Module configuration

---

# Layer Responsibility

## Controller Layer

Responsibilities:

* Receive HTTP requests
* Validate request parameters
* Call service methods
* Return API responses

Controller should NOT contain:

* Business logic
* Database queries
* Complex calculations

Example:

```text
GET /transactions

↓

TransactionController

↓

TransactionService
```

---

# Service Layer

The service layer contains all business logic.

Responsibilities:

* Process business rules
* Validate business conditions
* Coordinate multiple operations
* Handle transactions

Example:

```text
Create Transaction

↓

Check Account

↓

Validate Category

↓

Save Transaction

↓

Update Balance
```

---

# Prisma Layer

Prisma is responsible for database communication.

Responsibilities:

* CRUD operations
* Query relations
* Database transactions
* Data persistence

Flow:

```text
Service

↓

PrismaService

↓

PostgreSQL
```

---

# Database Access Strategy

Database access must go through PrismaService.

Incorrect:

```text
Controller

↓

Prisma

↓

Database
```

Correct:

```text
Controller

↓

Service

↓

Prisma

↓

Database
```

---

# Prisma ORM Design

Prisma schema is the single source of truth for database models.

Example:

```text
schema.prisma

model Transaction {

 id             String   @id @default(uuid())

 amount         Decimal

 type           String

 transactionDate DateTime

}
```

---

# DTO Design

DTOs are used for:

* Request validation
* Data transformation
* API contract definition

Example:

```text
CreateTransactionDto

UpdateTransactionDto

TransactionResponseDto
```

---

## Request DTO

Example:

```typescript
CreateTransactionDto

{
 amount,
 categoryId,
 accountId,
 transactionDate
}
```

---

## Response DTO

API responses should not expose database models directly.

Example:

```typescript
TransactionResponseDto

{
 id,
 amount,
 category,
 account,
 createdAt
}
```

---

# Validation

Validation uses:

* class-validator
* class-transformer

Example rules:

```text
amount

- Required
- Must be greater than 0

type

- Must be INCOME or EXPENSE
```

---

# Authentication & Authorization

Authentication uses JWT.

Flow:

```text
User Login

↓

Validate Credentials

↓

Generate JWT Token

↓

Client Sends Token

↓

JWT Guard

↓

Access Protected API
```

---

# JWT Structure

Token contains:

```json
{
 "sub": "user_id",
 "email": "user@email.com"
}
```

---

# Authorization

Authorization is handled through:

* Guards
* Decorators
* User roles (future)

---

# Error Handling

The backend uses centralized exception handling.

Components:

```text
Exception Filter

↓

Standard Error Response
```

---

## Error Response Format

```json
{
 "success": false,
 "errorCode": "TRANSACTION_NOT_FOUND",
 "message": "Transaction not found"
}
```

---

# HTTP Exception Mapping

| Exception                    | HTTP Status |
| ---------------------------- | ----------- |
| BadRequestException          | 400         |
| UnauthorizedException        | 401         |
| ForbiddenException           | 403         |
| NotFoundException            | 404         |
| ConflictException            | 409         |
| InternalServerErrorException | 500         |

---

# API Convention

RESTful API principles are applied.

## Resource Naming

Use plural nouns:

Correct:

```text
/transactions

/accounts

/categories
```

Incorrect:

```text
/getTransaction
/createAccount
```

---

# Pagination

List APIs support pagination.

Example:

```http
GET /transactions?page=1&size=20
```

Response:

```json
{
 "items": [],
 "page":1,
 "size":20,
 "totalItems":100
}
```

---

# Configuration Management

Environment variables:

```text
.env

DATABASE_URL

JWT_SECRET

JWT_EXPIRES_IN

PORT
```

Configuration is managed using:

```text
@nestjs/config
```

---

# Logging

Backend logging includes:

* Request information
* Error details
* Execution time
* Database errors

Recommended:

```text
NestJS Logger
```

---

# Testing Strategy

## Unit Testing

Test:

* Services
* Business rules
* Utility functions

## Integration Testing

Test:

* API endpoints
* Database interaction

## End-to-End Testing

Test:

* Complete user workflows

Example:

```text
Create Transaction

↓

View Dashboard

↓

Generate Report
```

---

# Coding Convention

## Naming

Classes:

```text
TransactionService

UserController
```

Files:

```text
transaction.service.ts

user.controller.ts
```

---

## General Rules

* Use TypeScript strict mode.
* Keep controllers lightweight.
* Put business logic in services.
* Use DTO for input/output.
* Avoid duplicated logic.
* Use dependency injection.
* Write reusable modules.

---

# Security Considerations

The backend must implement:

* JWT authentication
* Input validation
* SQL injection prevention through Prisma
* Environment variable protection
* CORS configuration
* Rate limiting (future)

---

# Performance Considerations

Optimization strategies:

* Database indexing
* Query optimization
* Pagination
* Select only required fields
* Avoid unnecessary relations
* Cache frequently accessed data (future)

---

# Future Improvements

Potential improvements:

* Redis caching
* Background jobs
* Message Queue
* File storage service
* Audit logging
* Role-based access control
* Microservice migration

---

# Summary

The backend follows a modular architecture based on NestJS principles.

Architecture:

```text
Controller

↓

Service

↓

Prisma ORM

↓

PostgreSQL
```

The design focuses on:

* Clean architecture
* Maintainability
* Scalability
* Security
* Developer productivity
