# System Architecture

## Overview

This document describes the overall system architecture of the **Personal Finance Tracker** application.

The system follows a modern full-stack architecture with a clear separation between:

* Frontend application
* Backend API service
* Database layer

The architecture focuses on:

* Maintainability
* Scalability
* Security
* Clear separation of responsibilities

---

# Tech Stack

## Frontend

* Next.js
* TypeScript
* Material UI
* TanStack Query

Responsibilities:

* User interface rendering
* User interaction handling
* Client-side navigation
* Server state management
* API communication

---

## Backend

* NestJS
* TypeScript

Responsibilities:

* REST API
* Business logic processing
* Authentication and authorization
* Data validation
* Communication with database

---

## Database

* PostgreSQL

Responsibilities:

* Persistent data storage
* Data consistency
* Relationship management
* Query processing

---

## ORM

* Prisma ORM

Responsibilities:

* Database access abstraction
* Type-safe queries
* Schema management
* Database migration

---

## Storage

MVP:

* Local Storage

Future:

* Object Storage (AWS S3 or equivalent)

Used for:

* Transaction attachments
* User uploaded files

---

## Deployment

MVP:

* Docker

Future:

* Cloud deployment
* CI/CD pipeline
* Container orchestration

---

# High-Level Architecture

```text
                 Browser

                    |

                    |

                Next.js

                    |

              REST API (HTTPS)

                    |

                    |

                NestJS API

                    |

                    |

                Prisma ORM

                    |

                    |

              PostgreSQL Database
```

---

# System Components

## Frontend Application

Technology:

* Next.js
* TypeScript
* Material UI
* TanStack Query

Responsibilities:

* Render user interface
* Handle user actions
* Fetch and cache server data
* Manage application state

Communication:

```text
Next.js

↓

REST API

↓

NestJS
```

---

## Backend Application

Technology:

* NestJS
* Prisma ORM

Responsibilities:

* Provide API endpoints
* Execute business rules
* Validate input
* Authenticate users
* Manage transactions

Architecture:

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

## Database Layer

Technology:

* PostgreSQL

Main entities:

```text
User

Account

Category

Transaction
```

Relationship:

```text
User

 |

 ├── Account

 |

 ├── Category

 |

 └── Transaction
```

---

# Request Flow

Example: Get transactions

```text
User

↓

Transaction Page

↓

TanStack Query

↓

API Service

↓

NestJS Controller

↓

Transaction Service

↓

Prisma Query

↓

PostgreSQL

↓

Response

↓

UI Update
```

---

# Authentication Flow

```text
User

↓

Login Page

↓

POST /auth/login

↓

NestJS Auth Module

↓

Validate Credentials

↓

Generate JWT

↓

Return Token

↓

Access Protected APIs
```

Protected request:

```text
Client

↓

JWT Token

↓

NestJS Guard

↓

Controller

↓

Service
```

---

# Data Flow

## Create Transaction

```text
User Input

↓

Frontend Form

↓

POST /transactions

↓

Transaction Controller

↓

Transaction Service

↓

Prisma Create

↓

PostgreSQL

↓

Return Response

↓

Update UI
```

---

# API Communication

Communication protocol:

```text
REST API
```

Transport:

```text
HTTPS
```

Data format:

```text
JSON
```

API Version:

```text
/api/v1
```

---

# Deployment Architecture

## MVP Deployment

```text
              User

               |

          Docker Container

               |

          Next.js Application

               |

          NestJS Application

               |

          PostgreSQL
```

---

# Security Architecture

## Application Security

* JWT Authentication
* Input validation
* Error handling
* CORS configuration

## Database Security

* Environment variables
* Restricted database access
* Prisma type-safe queries

## API Security

* Authentication middleware
* Request validation
* Rate limiting (future)

---

# Scalability Considerations

## Frontend

* Next.js optimization
* Code splitting
* Server rendering
* CDN support

## Backend

* Modular architecture
* Horizontal scaling
* Background processing

## Database

* Proper indexing
* Query optimization
* Database scaling

---

# Monitoring and Logging

Future implementation:

Backend:

* Application logs
* Error tracking
* Performance monitoring

Database:

* Query monitoring
* Slow query analysis

Frontend:

* Client error tracking
* Performance monitoring

---

# Future Improvements

* Cloud deployment
* CI/CD pipeline
* Redis caching
* Message queue
* File storage service
* Bank API integration
* AI financial insights
* Multi-user finance sharing

---

# Summary

The system follows the architecture:

```text
Browser

↓

Next.js

↓

NestJS API

↓

Prisma ORM

↓

PostgreSQL
```

This architecture provides:

* Clear separation of concerns
* Maintainable codebase
* Easy feature expansion
* Strong type safety
* Production-ready foundation
