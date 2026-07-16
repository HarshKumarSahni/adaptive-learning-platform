# Entity Relationship Diagram (ERD)

# Adaptive Learning Platform

Version: 1.0

---

# Purpose

This document defines the relationships between all entities in the database before implementation.

The ER Diagram is designed following Third Normal Form (3NF) and aims to minimize redundancy while maintaining scalability.

---

# Relationship Overview

## User Module

Role (1)
    ↓
User (N)

User (1)
    ↓
UserProfile (1)

User (1)
    ↓
UserSetting (1)

User (1)
    ↓
Bookmark (N)

User (1)
    ↓
Attempt (N)

User (1)
    ↓
Performance (1)

---

## Academic Module

Exam (1)
    ↓
Subject (N)

Subject (1)
    ↓
Chapter (N)

Chapter (1)
    ↓
Topic (N)

Topic (1)
    ↓
SubTopic (N)

SubTopic (N)
      ↕

QuestionSubTopic

      ↕

Question (N)

---

## Question Module

Question (1)
    ↓
QuestionOption (N)

Question (N)
    ↔
Test (N)

(using TestQuestion)

Question (N)
    ↔
Bookmark (N)

(via Bookmark table)

---

## Assessment Module

Test (1)
    ↓
TestConfiguration (1)

Test (1)
    ↓
Attempt (N)

Attempt (1)
    ↓
AttemptAnswer (N)

AttemptAnswer (N)
    ↓
Question (1)

---

## Analytics Module

User (1)
    ↓
Performance (1)

Performance (1)
    ↓
SubjectPerformance (N)

Performance (1)
    ↓
ChapterPerformance (N)

---

# Cardinality

Role
1 → N User

Exam
1 → N Subject

Subject
1 → N Chapter

Chapter
1 → N Topic

Topic
1 → N SubTopic

SubTopic
1 → N Question

Question
1 → N QuestionOption

Question
N ↔ N Test

Test
1 → N Attempt

Attempt
1 → N AttemptAnswer

User
1 → N Attempt

User
1 → N Bookmark

Question
1 → N Bookmark

---

# Junction Tables

TestQuestion

Purpose

Many-to-Many relationship

Between

Tests

Questions

---

# Future Relationships

Question
↓

AIRecommendation

↓

AIQuiz

↓

AIConversation

↓

AINote

↓

AIStudyPlan

The current schema allows these tables to be added without changing existing relationships.

---

# Design Principles

- No redundant foreign keys
- Immediate parent relationships only
- Junction tables for many-to-many relationships
- UUID primary keys
- Soft delete support
- Cascade rules where appropriate
- AI-ready architecture