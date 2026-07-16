# Database Indexing Strategy

# Adaptive Learning Platform

Version: 1.0

---

# Purpose

Indexes improve query performance by allowing PostgreSQL to locate rows quickly instead of scanning entire tables.

Indexes should only be added to columns that are frequently searched, filtered, sorted, or joined.

---

# User

## email

Type

Unique Index

Reason

Used during every login.

---

## roleId

Type

Index

Reason

Frequently used by admin queries.

---

# Subject

## examId

Reason

Retrieve all subjects for a particular exam.

---

# Chapter

## subjectId

Reason

Retrieve chapters for a subject.

---

# Topic

## chapterId

Reason

Retrieve topics for a chapter.

---

# SubTopic

## topicId

Reason

Retrieve subtopics for a topic.

---

# Question

## subTopicId

Reason

Most common filter.

---

## examId

Reason

Filter by exam.

---

## questionType

Reason

MCQ, Numerical, MSQ filtering.

---

## difficulty

Reason

Easy / Medium / Hard filtering.

---

## Composite Index

(subTopicId, questionType)

Reason

Generate topic-specific quizzes.

---

## Composite Index

(examId, difficulty)

Reason

Generate mock tests.

---

# Test

## createdBy

Reason

Retrieve admin-created tests.

---

# Attempt

## userId

Reason

Dashboard history.

---

## testId

Reason

View all attempts of a test.

---

## Composite Index

(userId, createdAt)

Reason

Recent activity.

---

# Bookmark

## Composite Unique Index

(userId, questionId)

Reason

Prevent duplicate bookmarks.

---

# Performance

## userId

Reason

Quick dashboard loading.

---

# Future AI

Future indexes may be added on

- AIConversation.userId
- AIRecommendation.userId
- AIStudyPlan.userId

---

# General Guidelines

- Index frequently searched columns.
- Avoid indexing low-cardinality columns.
- Use composite indexes only when query patterns justify them.
- Monitor query performance before adding additional indexes.