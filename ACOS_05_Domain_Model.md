
# ACOS - Domain Model
Version: 1.0

## Purpose

This document defines the business domains, bounded contexts, aggregates, entities,
value objects and relationships for the ACOS platform.

---

# 1. Domain-Driven Design Overview

ACOS follows a **Modular Monolith** with **Domain-Driven Design (DDD)**.

Each bounded context owns:
- Business rules
- Database tables
- REST APIs
- Services
- Events
- Documentation

---

# 2. Bounded Contexts

## Identity
Aggregate Roots
- User
- Role

Entities
- Permission
- UserSession

Value Objects
- Email
- PasswordHash

---

## Learning

Aggregate Roots
- LearningRoadmap
- StudyTask

Entities
- Milestone
- LearningJournal
- RevisionPlan

Value Objects
- StudyGoal
- StudyDuration

---

## Knowledge

Aggregate Root
- KnowledgeArticle

Entities
- Category
- Tag
- Attachment
- DiagramReference

Value Objects
- MarkdownContent
- SearchKeywords

---

## Interview

Aggregate Root
- InterviewQuestion

Entities
- ModelAnswer
- RevisionHistory
- MockInterview
- ConfidenceScore

---

## Portfolio

Aggregate Root
- Project

Entities
- ArchitectureArtifact
- GithubRepository
- LessonLearned
- DemoLink

---

## Career

Aggregate Root
- JobApplication

Entities
- Company
- Resume
- InterviewRound
- Offer

---

## Analytics

Aggregate Root
- DashboardSnapshot

Entities
- LearningMetric
- InterviewMetric
- PortfolioMetric

---

## AI

Aggregate Root
- PromptTemplate

Entities
- Agent
- Workflow
- EvaluationRun
- EmbeddingCollection

---

# 3. Cross-Domain Relationships

User
 ├── owns LearningRoadmaps
 ├── writes KnowledgeArticles
 ├── creates PortfolioProjects
 ├── tracks JobApplications
 ├── answers InterviewQuestions
 └── owns PromptTemplates

KnowledgeArticle
 ├── belongs to Category
 ├── has many Tags
 └── referenced by InterviewQuestion

PortfolioProject
 ├── references KnowledgeArticles
 ├── references ArchitectureArtifacts
 └── links Git Repository

---

# 4. Ubiquitous Language

Roadmap
Milestone
Study Task
Knowledge Article
Interview Question
Mock Interview
Portfolio Project
Architecture Artifact
Prompt
Workflow
Agent
Revision
Learning Journal

---

# 5. Domain Events (Future)

- UserRegistered
- RoadmapCompleted
- StudyTaskCompleted
- KnowledgeArticlePublished
- InterviewCompleted
- PortfolioPublished
- JobApplied
- ResumeUpdated

---

# 6. Ownership Rules

Identity owns authentication.

Learning owns study progress.

Knowledge owns technical content.

Interview owns interview preparation.

Portfolio owns showcase artifacts.

Career owns applications.

AI owns prompts, agents and evaluations.

---

# 7. Architect's Perspective

## Why DDD?

- Clear business boundaries
- High cohesion
- Low coupling
- Easier modularization
- Future microservice readiness

## Trade-offs

Pros
- Strong domain separation
- Easier maintenance
- Better scalability

Cons
- Higher initial design effort
- More concepts to learn

## Interview Questions

- What is a bounded context?
- Aggregate vs Entity?
- Why modular monolith?
- How would you split into microservices?
- Which aggregates should publish domain events?

---

# 8. Next Deliverables

1. Expanded HLD (C4)
2. Database ER Diagram
3. API Contracts
4. ADR-001 Modular Monolith
