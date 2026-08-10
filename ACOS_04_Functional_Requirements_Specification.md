
# ACOS - Book 1 : Product & Architecture
# 04 - Functional Requirements Specification (FRS)

**Version:** 1.0
**Status:** Draft

---

# 1. Purpose

This document defines the functional behavior of the Architect Career Operating System (ACOS).

Each requirement has a unique identifier that will be referenced by:
- HLD
- LLD
- Database Design
- API Design
- Test Cases
- Implementation Tasks

---

# 2. Requirement Traceability

| Module | Requirement IDs |
|---------|-----------------|
| Authentication | FR-AUTH-* |
| Dashboard | FR-DASH-* |
| Knowledge Base | FR-KB-* |
| Learning Roadmap | FR-LRN-* |
| Interview Bank | FR-INT-* |
| Portfolio | FR-PORT-* |
| Resume | FR-RES-* |
| Applications | FR-APP-* |
| Analytics | FR-ANA-* |

---

# 3. Authentication Module

## FR-AUTH-001
Users shall register using email and password.

Acceptance Criteria
- Email must be unique.
- Password follows policy.
- Email verification planned for future release.

---

## FR-AUTH-002
Users shall log in using JWT authentication.

Acceptance Criteria
- Access token returned.
- Refresh token supported.
- Invalid credentials return appropriate error.

---

## FR-AUTH-003
Users shall manage their profile.

Includes:
- Name
- Profile picture
- Target role
- Experience
- Skills

---

# 4. Dashboard Module

## FR-DASH-001
Display study progress.

## FR-DASH-002
Display interview readiness.

## FR-DASH-003
Display upcoming tasks.

## FR-DASH-004
Display recent activity.

Acceptance Criteria
- Dashboard loads in under 2 seconds under normal conditions.
- Widgets update without full page refresh where practical.

---

# 5. Knowledge Base

## FR-KB-001
Create article.

## FR-KB-002
Edit article.

## FR-KB-003
Delete article.

## FR-KB-004
Tag article.

## FR-KB-005
Search articles.

## FR-KB-006
Support Markdown.

Future
- Mermaid
- PlantUML
- Attachments
- Version history

---

# 6. Learning Roadmap

## FR-LRN-001
Create roadmap.

## FR-LRN-002
Create milestone.

## FR-LRN-003
Create study task.

## FR-LRN-004
Track completion.

## FR-LRN-005
Weekly review.

---

# 7. Interview Bank

## FR-INT-001
Create interview question.

## FR-INT-002
Categorize questions.

## FR-INT-003
Store model answers.

## FR-INT-004
Track confidence.

## FR-INT-005
Bookmark questions.

## FR-INT-006
Schedule revision.

---

# 8. Portfolio

## FR-PORT-001
Create project.

## FR-PORT-002
Store architecture diagrams.

## FR-PORT-003
Store GitHub repository.

## FR-PORT-004
Record lessons learned.

---

# 9. Resume

## FR-RES-001
Maintain multiple resume versions.

## FR-RES-002
Associate resumes with target companies.

---

# 10. Job Applications

## FR-APP-001
Track applications.

## FR-APP-002
Track interview rounds.

## FR-APP-003
Store recruiter feedback.

---

# 11. Analytics

## FR-ANA-001
Learning dashboard.

## FR-ANA-002
Study hours.

## FR-ANA-003
Readiness score.

## FR-ANA-004
Knowledge growth.

---

# 12. Validation Rules

- Required field validation
- Length validation
- Unique constraints
- Authorization checks
- Business rule validation

---

# 13. Roles

USER
ADMIN (future)

---

# 14. API Considerations

RESTful APIs

/api/v1/auth
/api/v1/dashboard
/api/v1/knowledge
/api/v1/roadmaps
/api/v1/interviews
/api/v1/projects

---

# 15. Database Implications

Primary entities:
- User
- KnowledgeArticle
- Roadmap
- StudyTask
- InterviewQuestion
- PortfolioProject
- Resume
- JobApplication

---

# 16. Test Scenarios

- Successful login
- Invalid login
- CRUD operations
- Authorization checks
- Validation failures
- Pagination
- Search
- Audit trail

---

# 17. Architect's Perspective

Why detailed FRS?

Because architecture should be traceable to requirements.

Interview Topics:
- Functional vs Non-functional requirements
- Acceptance criteria
- Traceability matrix
- Requirement prioritization
- MVP vs future scope

---

# 18. Next Document

05 - Non-Functional Requirements (NFR)

This will define:
- Performance
- Scalability
- Security
- Reliability
- Maintainability
- Observability
- Availability
- Disaster Recovery
- Compliance
