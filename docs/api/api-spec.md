# REST API Specification

# Adaptive Learning Platform

Version: 1.0

---

# API Principles

- RESTful
- Versioned APIs
- JSON Requests
- JSON Responses
- JWT Authentication
- Consistent Response Format
- Pagination Support
- Proper HTTP Status Codes

Base URL

/api/v1

---

# Authentication

POST /auth/register

POST /auth/login

POST /auth/logout

POST /auth/refresh-token

POST /auth/forgot-password

POST /auth/reset-password

GET /auth/me

PATCH /auth/change-password

---

# User

GET /users/profile

PATCH /users/profile

PATCH /users/settings

GET /users/bookmarks

POST /users/bookmarks

DELETE /users/bookmarks/{questionId}

---

# Exams

GET /exams

GET /exams/{id}

---

# Subjects

GET /subjects

GET /subjects/{id}

GET /subjects/{id}/chapters

---

# Chapters

GET /chapters

GET /chapters/{id}

GET /chapters/{id}/topics

---

# Topics

GET /topics

GET /topics/{id}

GET /topics/{id}/subtopics

---

# SubTopics

GET /subtopics

GET /subtopics/{id}

---

# Questions

GET /questions

GET /questions/{id}

POST /questions/search

---

# Tests

GET /tests

POST /tests/generate

GET /tests/{id}

POST /tests/start

POST /tests/submit

DELETE /tests/{id}

---

# Attempts

GET /attempts

GET /attempts/{id}

GET /attempts/history

---

# Analytics

GET /analytics/dashboard

GET /analytics/performance

GET /analytics/subjects

GET /analytics/chapters

---

# Admin

GET /admin/dashboard

POST /admin/exams

POST /admin/subjects

POST /admin/chapters

POST /admin/topics

POST /admin/subtopics

POST /admin/questions

PATCH /admin/questions/{id}

DELETE /admin/questions/{id}

POST /admin/tests

PATCH /admin/tests/{id}

DELETE /admin/tests/{id}

---

# Health

GET /health

---

# Future AI

POST /ai/chat

POST /ai/generate-test

POST /ai/generate-notes

POST /ai/recommendations

POST /ai/analyze

---

# Standard Response

Success

{
    "success": true,
    "message": "...",
    "data": {}
}

Error

{
    "success": false,
    "message": "...",
    "errors": []
}