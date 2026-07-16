# Entity Relationship Diagram (ERD)

# Adaptive Learning Platform

Version: 2.0

---

# Purpose

This document defines the logical relationships between all entities in the Adaptive Learning Platform.

The schema follows Third Normal Form (3NF), minimizes redundancy, and supports future AI integration without major structural changes.

---

# User Module

Role (1)
    │
    └──────────────▶ User (N)

User (1)
    │
    ├──────────────▶ UserProfile (1)
    │
    ├──────────────▶ UserSetting (1)
    │
    ├──────────────▶ Bookmark (N)
    │
    ├──────────────▶ Attempt (N)
    │
    └──────────────▶ Performance (1)

---

# Academic Module

Exam (N)
      ▲
      │
ExamSubject
      │
      ▼
Subject (N)

Subject (1)
      │
      ▼
Chapter (N)

Chapter (1)
      │
      ▼
Topic (N)

Topic (1)
      │
      ▼
SubTopic (N)

---

# Question Module

Question (N)
      ▲
      │
QuestionSubTopic
      │
      ▼
SubTopic (N)

Question (N)
      ▲
      │
QuestionExam
      │
      ▼
Exam (N)

Question (1)
      │
      ├────────────▶ QuestionOption (N)
      │
      ├────────────▶ QuestionImage (N)
      │
      ├────────────▶ QuestionExplanation (1)
      │
      └────────────▶ QuestionTag (N)

---

# Assessment Module

Test (1)
      │
      ├────────────▶ TestConfiguration (1)
      │
      ├────────────▶ Attempt (N)
      │
      ▼
TestQuestion
      ▲
      │
Question (N)

Attempt (1)
      │
      ▼
AttemptAnswer (N)

AttemptAnswer (N)
      │
      ▼
Question (1)

---

# Analytics Module

User (1)
      │
      ▼
Performance (1)

Performance (1)
      │
      ├────────────▶ SubjectPerformance (N)
      │
      └────────────▶ ChapterPerformance (N)

---

# Bookmark Module

User (1)
      │
      ▼
Bookmark (N)
      ▲
      │
Question (1)

A user may bookmark the same question only once.

---

# Junction Tables

## ExamSubject

Purpose

Maps Subjects to multiple Exams.

Examples

Physics

↓

CBSE Class 12

↓

JEE Main

↓

JEE Advanced

---

## QuestionExam

Purpose

Maps Questions to one or more Exams.

Examples

Question 101

↓

CBSE 2024

↓

JEE Main 2025

---

## QuestionSubTopic

Purpose

Maps Questions to one or more SubTopics.

Examples

Question

↓

Electric Field

↓

Gauss Law

↓

Electric Potential

---

## TestQuestion

Purpose

Many-to-Many relationship between

Tests

Questions

---

# Cardinality Summary

Role
1 → N User

Exam
N ↔ N Subject

Subject
1 → N Chapter

Chapter
1 → N Topic

Topic
1 → N SubTopic

Question
N ↔ N SubTopic

Question
N ↔ N Exam

Question
1 → N QuestionOption

Question
1 → N QuestionImage

Question
1 → 1 QuestionExplanation

Question
1 → N QuestionTag

Test
N ↔ N Question

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

User
1 → 1 Performance

Performance
1 → N SubjectPerformance

Performance
1 → N ChapterPerformance

---

# Future AI Relationships

Question
      │
      ├────────────▶ AIRecommendation
      │
      ├────────────▶ AIQuiz
      │
      ├────────────▶ AIWeakTopic
      │
      ├────────────▶ AIConversation
      │
      └────────────▶ AINote

These entities will be implemented as separate modules and do not require modification to the existing schema.

---

# Design Principles

- UUID Primary Keys
- Third Normal Form (3NF)
- Immediate Parent Relationships
- Many-to-Many via Junction Tables
- Soft Delete Support
- Audit Fields
- AI-Ready Architecture
- Extensible for New Exams
- Optimized for Read Performance