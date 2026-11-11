# Design Freeze

**Document Version:** v1.0
**Status:** Frozen
**Last Updated:** 2026-07-16

---

# 1. Purpose

This document marks the completion of the system design phase.

From this point onward, all implementation activities must follow the approved design documents.

Design changes should be avoided during implementation unless a significant architectural issue or new business requirement is identified.

Any approved design changes must be recorded in a new document version (for example, v1.1).

---

# 2. Design Phase Completion

The following design documents have been reviewed and approved.

| Document            | Status      |
| ------------------- | ----------- |
| Project Overview    | ✅ Completed |
| Requirements        | ✅ Completed |
| Business Flow       | ✅ Completed |
| Database Design     | ✅ Completed |
| API Design          | ✅ Completed |
| Frontend Design     | ✅ Completed |
| System Architecture | ✅ Completed |

---

# 3. Source of Truth

The following documents are considered the official design reference for implementation.

* Project Overview
* Requirements
* Business Flow
* Database Design
* API Design
* Frontend Design
* System Architecture

Developers must follow these documents when implementing the system.

---

# 4. Approved Design Decisions

The following architectural decisions have been finalized.

## General

* Backend: NestJS
* Frontend: Next.js
* Database: PostgreSQL
* ORM & Migration: Prisma
* Deployment: Docker

---

## Database

* UUID is used as the primary key.
* All timestamps are stored in UTC.
* Monetary values use Decimal.
* Transaction time is nullable.
* Categories do not contain transaction type.
* Transaction type is stored only in Transactions.
* Dashboard calculations belong to the Backend.

---

## API

* RESTful API
* Plural resource naming
* PATCH for partial updates
* GET for read-only operations
* Dashboard exposes read-only APIs
* Transaction Enrichment is an independent module

---

## Frontend

* Frontend is responsible for presentation only.
* Business rules and analytics are implemented in the Backend.
* Dashboard only renders processed data.

---

# 5. Out of Scope

The following features are intentionally excluded from the current implementation phase.

* AI Insights
* OCR Processing
* Multi-bank Support
* Budget Planning
* Investment Management
* Advanced Financial Reports

These features may be introduced in future versions.

---

# 6. Implementation Entry Criteria

Implementation may begin after confirming that:

* Database schema is finalized.
* API inventory is finalized.
* Frontend design is finalized.
* Module boundaries are clearly defined.
* No critical design issues remain unresolved.

---

# 7. Next Phase

The project now moves from the Design phase to the Implementation phase.

Implementation will proceed according to the following order:

1. Backend Foundation
2. Authentication & User
3. Account
4. Category
5. Transaction
6. Import
7. Category Rule
8. Dashboard
9. Transaction Enrichment

The implementation process is described in the Backend Implementation Plan and Frontend Implementation Plan.

---

# 8. Change Management

After Design Freeze, design modifications should be minimized.

If a design change is required:

1. Identify the reason for the change.
2. Evaluate the architectural impact.
3. Update the affected design document.
4. Increase the document version.
5. Communicate the change before implementation continues.

No implementation should diverge from the approved design without updating the corresponding design documentation.
