# Low Level Design (LLD)

# Adaptive Learning Platform

Version 1.0

---

# Purpose

This document describes the internal software architecture of the Adaptive Learning Platform.

Unlike the High Level Design, this document focuses on modules, layers, responsibilities, request flow, class interactions, and design patterns.

---

# Backend Architecture

The backend follows Clean Architecture.

Request

↓

Route

↓

Middleware

↓

Controller

↓

Service

↓

Repository

↓

Prisma ORM

↓

PostgreSQL

---

# Layer Responsibilities

## Routes

Responsibilities

- Define API endpoints
- Apply middleware
- Forward requests to controllers

Business logic should never exist here.

---

## Middleware

Responsibilities

- Authentication
- Authorization
- Validation
- Rate Limiting
- Logging
- Error Handling

---

## Controllers

Responsibilities

- Receive validated requests
- Call service layer
- Return API responses

Controllers must remain thin.

---

## Services

Responsibilities

- Business Logic
- Workflow orchestration
- Validation beyond request level
- Transaction management

Services should contain all business rules.

---

## Repository Layer

Responsibilities

- Database access
- Prisma queries
- Query optimization

Repositories isolate the database implementation.

---

## Prisma ORM

Responsibilities

- Mapping objects to PostgreSQL
- Migrations
- Relations
- Transactions

---

## Database

Responsibilities

Store:

- Users
- Subjects
- Chapters
- Questions
- Tests
- Attempts
- Analytics

---

# Frontend Architecture

Feature Based Architecture

app/

↓

features/

↓

components/

↓

hooks/

↓

services/

↓

API

Each feature remains independent.

---

# Folder Structure

Frontend

app/

components/

features/

hooks/

providers/

services/

types/

utils/

Backend

controllers/

routes/

services/

repositories/

middlewares/

validators/

dto/

config/

lib/

types/

utils/

errors/

---

# Authentication Flow

Client

↓

POST /login

↓

Validate Request

↓

Controller

↓

Auth Service

↓

User Repository

↓

PostgreSQL

↓

Verify Password

↓

Generate JWT

↓

Return Tokens

---

# Quiz Flow

Student

↓

Start Quiz

↓

Create Attempt

↓

Fetch Questions

↓

Save Answers

↓

Submit Quiz

↓

Evaluation

↓

Performance Update

↓

Dashboard Refresh

---

# Admin Flow

Admin

↓

Create Subject

↓

Create Chapter

↓

Upload Questions

↓

Create Mock Test

↓

Publish

↓

Students Access Content

---

# Error Handling

Global Error Handler

↓

Custom Error Classes

↓

Consistent API Response

---

# Logging

Every request should log:

- Request ID
- Endpoint
- Method
- Response Time
- Status Code

---

# Design Patterns

Repository Pattern

Service Pattern

Factory Pattern (Future Question Generator)

Strategy Pattern (Evaluation Engine)

Builder Pattern (Test Creation)

Observer Pattern (Notifications)

Singleton Pattern (Logger)

---

# Security

JWT Authentication

Role Based Access Control

Password Hashing

Rate Limiting

Helmet

Zod Validation

CORS

Environment Validation

---

# Future AI Integration

Current Architecture

Frontend

↓

Backend

↓

Database

Future

Frontend

↓

Backend

↓

AI Gateway

↓

FastAPI

↓

LLM

↓

Response

The AI service remains independent and can be deployed separately without changing existing modules.