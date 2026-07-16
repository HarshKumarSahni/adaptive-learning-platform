# Database Design

# Adaptive Learning Platform

Version: 2.0

---

# Purpose

This document defines the logical database design for the Adaptive Learning Platform.

The database is designed using PostgreSQL and follows Third Normal Form (3NF). The schema is modular, scalable, and AI-ready.

---

# Design Principles

- PostgreSQL
- UUID Primary Keys
- Normalized Schema (3NF)
- Foreign Key Constraints
- Soft Deletes
- Audit Fields
- AI-Ready
- Extensible for New Exams

---

# Entity Categories

## User Management

- User
- Role
- UserProfile
- UserSetting
- Bookmark

---

## Academic Structure

- Exam
- Subject
- Chapter
- Topic
- SubTopic

---

## Question Bank

- Question
- QuestionOption
- QuestionTag
- QuestionExplanation

---

## Assessment

- Test
- TestConfiguration
- TestQuestion
- Attempt
- AttemptAnswer

---

## Analytics

- Performance
- SubjectPerformance
- ChapterPerformance

---

# Entity Details

---

## Role

Purpose

Defines user permissions.

Examples

- Student
- Admin
- Teacher (Future)
- Moderator (Future)

Attributes

- id
- name
- description

---

## User

Purpose

Stores user account information.

Attributes

- id
- fullName
- email
- passwordHash
- roleId
- profileImage
- isVerified
- isActive
- createdAt
- updatedAt
- deletedAt

Relationships

- belongs to Role
- has one UserProfile
- has one UserSetting
- has many Attempts
- has many Bookmarks

---

## Exam

Purpose

Defines which examination a question belongs to.

Examples

- CBSE Class 10
- CBSE Class 12
- ICSE Class 10
- ICSE Class 12
- JEE Main
- JEE Advanced

Attributes

- id
- name
- category (Board / Competitive)
- description

Relationships

- has many Subjects
- has many Questions

---

## Subject

Examples

Physics

Chemistry

Mathematics

Biology (Future)

Attributes

- id
- examId
- name

Relationships

- belongs to Exam
- has many Chapters

---

## Chapter

Attributes

- id
- subjectId
- name
- order

Relationships

- belongs to Subject
- has many Topics

---

## Topic

Attributes

- id
- chapterId
- name
- order

Relationships

- belongs to Chapter
- has many SubTopics

---

## SubTopic

Attributes

- id
- topicId
- name
- order

Relationships

- belongs to Topic
- has many Questions

---

## Question

Purpose

Stores every question in the platform.

Supported Types

- MCQ
- MSQ
- Numerical
- Short Answer
- Long Answer
- Fill in the Blank

Attributes

- id
- subTopicId
- examId
- questionType
- difficulty
- marks
- negativeMarks
- questionText
- explanation
- source
- year
- suitableForClass (10 / 11 / 12 / 11+12)
- isPreviousYear
- estimatedTime

Relationships

- belongs to many Exams (via QuestionExam)
- belongs to many SubTopics (via QuestionSubTopic)
- has many QuestionOptions
- belongs to many Tests (via TestQuestion)
- has many Tags (via QuestionTag)

---

## QuestionOption

Purpose

Stores answer choices.

Attributes

- id
- questionId
- optionLabel
- optionText
- isCorrect

---

## QuestionExam

Purpose

Maps questions to one or more exams.

Examples

A question may belong to:

- CBSE Class 12
- JEE Main

Attributes

- questionId
- examId

Relationships

- belongs to Question
- belongs to Exam

---

## QuestionSubTopic

Purpose

Maps questions to one or more subtopics.

Examples

A question may belong to:

- Electric Field
- Gauss Law

Attributes

- questionId
- subTopicId

Relationships

- belongs to Question
- belongs to SubTopic

---

## QuestionTag

Purpose

Stores tags for searching and filtering.

Examples

- Formula Based
- PYQ
- Easy
- Important

Attributes

- questionId
- tag

Relationships

- belongs to Question

---

## Test

Purpose

Represents a student-created or admin-created assessment.

Attributes

- id
- title
- createdBy
- duration
- totalMarks
- testType

Examples

- Practice Quiz
- Chapter Test
- Mock Test
- Previous Year Test
- Custom Test

Relationships

- has one TestConfiguration
- has many TestQuestions
- has many Attempts

---

## TestConfiguration

Purpose

Stores the rules used to generate a test.

Attributes

- id
- testId
- selectedExam
- selectedSubjects
- selectedChapters
- selectedTopics
- selectedSubTopics
- questionTypes
- difficultyLevels
- totalQuestions
- duration

This allows future AI-generated tests without changing the database.

---

## TestQuestion

Purpose

Many-to-many relationship between Tests and Questions.

---

## Attempt

Attributes

- id
- userId
- testId
- startedAt
- submittedAt
- score
- percentage

Relationships

- belongs to User
- belongs to Test
- has many AttemptAnswers

---

## AttemptAnswer

Attributes

- id
- attemptId
- questionId
- selectedAnswer
- isCorrect
- marksAwarded
- timeTaken

---

## Performance

Purpose

Stores aggregated performance statistics.

Attributes

- id
- userId
- averageScore
- accuracy
- testsCompleted
- averageTimePerQuestion

---

## Bookmark

Purpose

Stores saved questions.

Attributes

- id
- userId
- questionId

---

# Future Entities

- AIConversation
- AIRecommendation
- AIStudyPlan
- AIQuiz
- AINote
- Notification
- Achievement
- Feedback
- Report