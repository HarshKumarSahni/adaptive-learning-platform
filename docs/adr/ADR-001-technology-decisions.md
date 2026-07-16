# ADR-001 — Technology Decisions

Status: Accepted

---

# Context

The Adaptive Learning Platform aims to be a production-ready educational SaaS application that demonstrates modern software engineering practices while remaining scalable for future AI integration.

This document records the reasons behind major architectural decisions.

---

# Why Next.js?

Decision

Use Next.js instead of React + Vite.

Reason

- File-based routing
- Better SEO
- Server Components support
- Easy deployment on Vercel
- Industry adoption

---

# Why TypeScript?

Decision

Use TypeScript across frontend and backend.

Reason

- Type safety
- Better IDE support
- Easier refactoring
- Fewer runtime bugs

---

# Why Express instead of NestJS?

Decision

Use Express.

Reason

- Lower learning curve
- Better understanding of backend fundamentals
- More flexibility
- Easier to explain in interviews

Future

The architecture remains compatible with migration to NestJS.

---

# Why PostgreSQL?

Decision

Use PostgreSQL instead of MongoDB.

Reason

- Strong relational support
- ACID compliance
- Complex joins
- Better analytics
- Industry standard

---

# Why Prisma?

Decision

Use Prisma ORM.

Reason

- Excellent TypeScript support
- Easy migrations
- Type-safe queries
- Modern developer experience

---

# Why Redis?

Decision

Use Redis for caching.

Reason

- Reduce database load
- Improve dashboard performance
- Cache leaderboards
- Cache frequently accessed content

---

# Why JWT?

Decision

JWT Authentication.

Reason

- Stateless authentication
- Easy frontend integration
- Suitable for REST APIs

Future

Refresh token rotation will be implemented.

---

# Why REST instead of GraphQL?

Decision

Use REST APIs.

Reason

- Simpler architecture
- Easier debugging
- Better for learning backend fundamentals
- Suitable for current requirements

Future

GraphQL Gateway can be introduced.

---

# Why Modular Monolith?

Decision

Start as a modular monolith.

Reason

- Easier deployment
- Easier debugging
- Faster development
- Lower operational complexity

Future

AI module can become an independent microservice.

---

# Why Clean Architecture?

Decision

Separate business logic from infrastructure.

Reason

- Easier testing
- Better maintainability
- Loose coupling
- Scalable codebase

---

# Why Repository Pattern?

Decision

Repositories handle database access.

Reason

- Database abstraction
- Easier testing
- Cleaner services

---

# Why Service Layer?

Decision

Business logic belongs only in services.

Reason

- Controllers remain thin
- Better separation of concerns
- Easier maintenance

---

# Future AI Integration

Decision

AI will be implemented as a separate service.

Reason

- Independent deployment
- Independent scaling
- Better fault isolation
- Easier maintenance