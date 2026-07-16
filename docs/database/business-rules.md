# Business Rules

# Adaptive Learning Platform

Version: 1.1

---

# Purpose

This document defines business constraints enforced by the application.

Unlike database constraints, these rules are validated in the Service Layer.

---

# Authentication Rules

- Every email must be unique.
- Passwords must be hashed before storage.
- Unverified users cannot login.
- Suspended users cannot access the platform.
- JWT Access Tokens expire after the configured duration.
- Refresh Tokens must be rotated.

---

# User Rules

- A user must have exactly one role.
- Every user has one profile.
- Every user has one settings record.
- Every user can bookmark the same question only once.
- A user may prepare for multiple exams simultaneously (e.g., CBSE Class 12 and JEE Main).

---

# Academic Rules

- Subjects are independent academic entities.
- An Exam can contain multiple Subjects.
- A Subject can belong to multiple Exams.
- This relationship is managed using the **ExamSubject** junction table.

- Every Chapter belongs to one Subject.
- Every Topic belongs to one Chapter.
- Every SubTopic belongs to one Topic.

---

# Question Rules

- Every Question must belong to at least one Exam.
- Every Question must belong to one or more SubTopics.
- Multiple SubTopics are managed using the **QuestionSubTopic** junction table.

MCQ

- Must have at least two options.
- Must have at least one correct option.

MSQ

- Must have at least two correct options.

Numerical

- Must not have QuestionOptions.
- Must contain exactly one numeric answer.

Short Answer

- Must contain a reference answer.

Long Answer

- Must contain an evaluation rubric.

Fill in the Blank

- Must contain one or more accepted answers.

---

# Test Rules

Every Test

- Must contain at least one question.
- Must have a positive duration.
- Must have positive total marks.

Custom Test

The student may configure a test using:

- One or more Exams
- One or more Subjects
- One or more Chapters
- One or more Topics
- One or more SubTopics
- One or more Question Types
- Difficulty Levels
- Number of Questions
- Duration

The system generates a test matching the selected configuration.

Previous Year Test

- Questions must belong to the selected exam(s).
- Questions must match the selected year(s).

---

# Attempt Rules

- A student cannot have two active attempts for the same test.
- Once submitted, an attempt cannot be modified.
- Auto-submit occurs when the timer expires.
- Every answer belongs to one attempt.

---

# Bookmark Rules

- Duplicate bookmarks are not allowed.
- Deleting a question removes related bookmarks.

---

# Analytics Rules

- Performance updates only after successful submission.
- Analytics are calculated from Attempt records.
- Performance is never manually edited.

---

# Admin Rules

Only Admins can:

- Create Subjects
- Create Chapters
- Create Topics
- Create SubTopics
- Create Questions
- Publish Tests
- Delete Questions

---

# Teacher Rules (Future)

Teachers may:

- Create Notes
- Create Practice Tests
- View Student Progress

Teachers cannot:

- Delete Platform Questions.

---

# AI Rules (Future)

- AI cannot directly modify database records.
- Every AI-generated question must be reviewed before publishing.
- AI recommendations remain advisory.

---

# Soft Delete Rules

Soft deleted entities:

- cannot appear in normal API responses.
- remain available for auditing.
- preserve historical relationships.

---

# Audit Rules

Every important operation should be logged:

- Login
- Question Creation
- Test Creation
- Test Submission
- Admin Actions

---

# Validation Flow

Every request follows:

Input Validation

↓

Authentication

↓

Authorization

↓

Business Rule Validation

↓

Database