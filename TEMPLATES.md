# Document Templates

Structural specs for each document type. Every template defines required sections, visual element positions, and common pitfalls.

All templates are tech-stack agnostic. Fill in specific technologies only when the document's purpose requires it (setup guides, dependency lists).

---

## product-requirements (PRD)

**Purpose:** Define what to build and why. Features, user stories, acceptance criteria.

**Required Sections:**

```markdown
# [Product/Feature Name]

## Problem Statement
What problem does this solve? Who has this problem? How do they cope today?
[DIAGRAM: user journey showing current pain points]

## Target Users
User personas with concrete behaviors, not demographics.
[TABLE: persona | core need | current workaround | success metric]

## Goals & Non-Goals
What this release does. What it explicitly does NOT do.
[TABLE: goal | success metric | target value | measurement method]

## Feature Specifications
For each feature:
### Feature: [Name]
**User story:** As a [role], I want [action] so that [outcome].
**Acceptance criteria:**
- Given [context], when [action], then [result]
[DIAGRAM: mermaid flowchart — user interaction flow for this feature]

## Data Requirements
What data is collected, stored, displayed, exported.
[TABLE: data field | source | format | validation rules | privacy classification]

## Non-Functional Requirements
Performance, security, accessibility, compatibility.
[TABLE: category | requirement | target value | measurement method]

## Out of Scope
Explicitly excluded features. Brief reason for each.
```

**Visual Requirements:** ≥ 1 user flow diagram, ≥ 1 comparison table per major feature, ≥ 1 data model diagram if data-heavy.

**Common Pitfalls:** Vague acceptance criteria ("the system should be fast"). No non-goals section (scope creep). Mixing implementation details with requirements.

---

## architecture-doc

**Purpose:** System overview, component relationships, technology decisions.

**Required Sections:**

```markdown
# [System Name] Architecture

## System Context
What is this system? What external systems does it interact with?
[DIAGRAM: mermaid graph — system context diagram with external actors]

## Component Overview
Internal components and their responsibilities.
[DIAGRAM: mermaid graph TD — component diagram with connections labeled by protocol/data format]

## Data Flow
How data moves through the system.
[DIAGRAM: mermaid sequenceDiagram — key request/response flow]

## Data Model
Entity relationships and storage strategy.
[DIAGRAM: mermaid erDiagram — entity relationships]
[TABLE: entity | primary key | relationships | storage type | index strategy]

## API Boundaries
External and internal API contracts.
[TABLE: endpoint | method | purpose | auth required | rate limit]

## Technology Decisions
[TABLE: decision | option A | option B | chosen | reason]

## Security Model
Authentication, authorization, data protection.
[DIAGRAM: mermaid flowchart — auth decision flow]

## Deployment Topology
Where components run and how they connect.
[DIAGRAM: mermaid graph — infrastructure layout]

## Scaling Strategy
How the system handles growth.
[TABLE: component | current capacity | bottleneck | scaling approach | trigger threshold]

## Known Limitations
What the architecture cannot do today.
```

**Visual Requirements:** ≥ 1 context diagram, ≥ 1 component diagram, ≥ 1 sequence diagram, ≥ 1 ER diagram. Architecture docs without diagrams are useless.

**Common Pitfalls:** Listing technologies without explaining WHY. No data flow diagram (just static component boxes). Ignoring failure modes.

---

## adr (Architecture Decision Record)

**Purpose:** Record why a specific technical decision was made.

**Required Sections:**

```markdown
# ADR-[N]: [Decision Title]

## Status
[Proposed | Accepted | Deprecated | Superseded by ADR-X]

## Context
What is the issue? What forces are at play?
[TABLE: factor | constraint | impact]

## Decision
The chosen approach, stated in one sentence. Then the details.

## Alternatives Considered
[TABLE: alternative | pros | cons | why rejected]

## Consequences
[TABLE: consequence | type (positive/negative) | mitigation]

## Implementation Notes
Key details for executing this decision.
```

**Visual Requirements:** Decision comparison table is mandatory. Flowchart if the decision involves a process change.

**Common Pitfalls:** Not listing alternatives. Not recording WHY alternatives were rejected (the most valuable part).

---

## api-spec

**Purpose:** Endpoint contracts — request/response formats, authentication, error codes.

**Required Sections:**

```markdown
# [Service Name] API

## Authentication
How to authenticate. Token format, expiry, refresh mechanism.

## Base URL
Environment-specific base URLs.
[TABLE: environment | base URL | notes]

## Endpoints
For each endpoint:
### [METHOD] [path]
**Purpose:** One sentence.
**Auth:** Required / Optional / None

**Request:**
[TABLE: parameter | location | type | required | description | example]

**Response (200):**
[TABLE: field | type | description | example]

**Error Responses:**
[TABLE: status code | error code | description | resolution]

**Example:**
```http
[complete request and response example]
```

## Rate Limiting
[TABLE: tier | limit | window | header]

## Pagination
Strategy (cursor/offset), parameters, response format.

## Versioning
How API versions are managed and deprecated.
```

**Visual Requirements:** ≥ 1 sequence diagram for the most complex flow. Request/response tables for every endpoint.

**Common Pitfalls:** Missing error responses. No example request/response. Vague parameter descriptions ("the user's name").

---

## database-design

**Purpose:** Schema, relationships, indexing, migration strategy.

**Required Sections:**

```markdown
# [Database Name] Design

## Entity Overview
[DIAGRAM: mermaid erDiagram — all entities and relationships]

## Table Specifications
For each table:
### [table_name]
**Purpose:** One sentence.
[TABLE: column | type | nullable | default | description]
[TABLE: index | columns | type | purpose]

## Relationships
[TABLE: from | to | type | cascade rules]
[DIAGRAM: mermaid flowchart — foreign key dependency graph]

## Migration Strategy
How schema changes are deployed. Order of operations. Rollback plan.

## Performance Considerations
[TABLE: query pattern | tables involved | expected rows | index strategy | target latency]
```

**Visual Requirements:** ER diagram is mandatory. Migration dependency graph for complex schemas.

---

## readme

**Purpose:** Project overview, setup instructions, how to run and contribute.

**Required Sections:**

```markdown
# [Project Name]

One-paragraph description of what this project does and why it exists.

## Quick Start
Minimum steps to get running. 3-5 steps max.
```bash
[exact commands to install and run]
```
Expected output:
```
[what the user should see]
```

## Prerequisites
[TABLE: dependency | minimum version | install command | purpose]

## Project Structure
```
[directory tree with brief annotation per directory]
```

## Configuration
[TABLE: env variable | required | default | description]

## Development
How to run tests, lint, build.
```bash
[exact commands]
```

## Contributing
How to submit changes. Link to coding standards if separate.

## License
```

**Visual Requirements:** Directory tree. Dependency table. No diagrams needed unless the project is a library/framework.

**Common Pitfalls:** No "Quick Start" section. Missing expected output after commands. Outdated dependency versions.

---

## deployment-guide

**Purpose:** Step-by-step deployment process, rollback, environment setup.

**Required Sections:**

```markdown
# Deployment Guide: [Service Name]

## Prerequisites
[TABLE: requirement | version | verification command]

## Environment Setup
[TABLE: environment | URL | database | notes]

## Deployment Steps
Numbered steps. Each step is one atomic action.
[DIAGRAM: mermaid flowchart — deployment pipeline stages]

### Step 1: [Action]
```bash
[exact command]
```
Expected: [what success looks like]

### Step 2: [Action]
...

## Verification
Post-deployment checks.
[TABLE: check | command | expected result | if fails]

## Rollback
Step-by-step rollback procedure.
[DIAGRAM: mermaid flowchart — rollback decision tree]

## Monitoring
Post-deployment monitoring checklist.
[TABLE: metric | dashboard URL | alert threshold | action if breached]
```

**Visual Requirements:** Deployment pipeline flowchart. Rollback decision tree. Verification table.

**Common Pitfalls:** No rollback procedure. No expected output after commands. No verification step.

---

## changelog

**Purpose:** What changed in each version.

**Required Sections:**

```markdown
# Changelog

## [version] — [date]
### Added
- [feature] — [brief description] ([issue/PR link])

### Changed
- [change] — [what changed and why]

### Fixed
- [bug] — [what was broken, what fixes it]

### Removed
- [removal] — [why, migration path]

### Security
- [vulnerability] — [severity, fix, CVE if applicable]
```

**Format Rules:**
- Follow "Keep a Changelog" format
- Each entry is one line. No paragraphs.
- Link to issue/PR where applicable
- Group by change type: Added, Changed, Fixed, Removed, Security
- Newest version first

---

## user-guide

**Purpose:** Complete usage reference for end users.

**Required Sections:**

```markdown
# [Product Name] User Guide

## Getting Started
What this product does. Who it's for. 5-minute setup.
[DIAGRAM: mermaid flowchart — core user workflow]

## Core Concepts
[TABLE: concept | definition | example]

## Feature Guides
For each major feature:
### [Feature Name]
What it does. When to use it.
Step-by-step instructions with screenshots or diagrams.
[DIAGRAM: mermaid sequenceDiagram — user interaction flow]
[TABLE: option | values | default | effect]

## Troubleshooting
[TABLE: symptom | possible cause | resolution]

## Glossary
[TABLE: term | definition]
```

**Visual Requirements:** ≥ 1 workflow diagram per major feature. Troubleshooting table. Options/parameters table.

---

## postmortem

**Purpose:** What happened during an incident, why, and how to prevent recurrence.

**Required Sections:**

```markdown
# Post-Mortem: [Incident Name] — [Date]

## Summary
What happened, in 2-3 sentences. Impact duration and scope.
[TABLE: metric | value | notes]

## Timeline
[TABLE: timestamp (UTC) | event | actor | detection method]
[DIAGRAM: mermaid gantt — incident timeline]

## Root Cause
The actual technical root cause. Not "human error."
[DIAGRAM: mermaid flowchart — causal chain]

## What Went Well
Specific things that helped contain or resolve the incident.

## What Went Wrong
Specific gaps. Not vague "we need better monitoring."

## Action Items
[TABLE: action | owner | priority | due date | status]

## Lessons Learned
What we'll do differently going forward.
```

**Visual Requirements:** Incident timeline (Gantt or table). Causal chain diagram. Action items table.

**Common Pitfalls:** Blaming people instead of systems. Vague action items ("improve monitoring"). Missing timeline.

---

## test-plan

**Purpose:** Testing strategy, scope, environments, entry/exit criteria.

**Required Sections:**

```markdown
# Test Plan: [Feature/Release Name]

## Scope
[TABLE: area | in scope | out of scope | reason]

## Test Strategy
[TABLE: test type | scope | tool | responsible | schedule]

## Test Cases
[TABLE: ID | scenario | preconditions | steps | expected result | priority]

## Environments
[TABLE: environment | URL | database | test data | notes]

## Entry / Exit Criteria
**Entry:** [conditions that must be true before testing begins]
**Exit:** [conditions that must be true before declaring testing complete]

## Risk Assessment
[TABLE: risk | probability | impact | mitigation]
```

**Visual Requirements:** Scope table. Test strategy matrix. Risk assessment table.

---

## coding-standards

**Purpose:** Team conventions — naming, style, folder structure, review process.

**Required Sections:**

```markdown
# Coding Standards

## Naming Conventions
[TABLE: entity | convention | example | anti-example]

## File Organization
```
[project directory structure with annotations]
```

## Code Style
Key rules with before/after examples.
[TABLE: rule | bad example | good example]

## Error Handling
Strategy, patterns, what to log, what to swallow.

## Testing Conventions
File naming, test structure, what to test, coverage expectations.

## Git Workflow
Branch naming, commit message format, PR process.
[TABLE: commit type | prefix | example]

## Review Checklist
[TABLE: check | description | severity (block/warn)]
```

**Visual Requirements:** Naming convention table. Directory tree. Before/after code examples.

---

## quickstart

**Purpose:** Get the user from zero to working in under 5 minutes.

**Required Sections:**

```markdown
# Quick Start

## What You'll Build
One sentence + one screenshot or diagram.
[DIAGRAM: mermaid graph — final result overview]

## Prerequisites
[TABLE: requirement | version | install command]

## Steps
Numbered. Each step is one command or one action.
### Step 1: [Action]
```bash
[exact command]
```
Expected:
```
[exact output]
```

### Step 2: [Action]
...

## Next Steps
2-3 links to deeper documentation.
```

**Visual Requirements:** Prerequisites table. Expected output after every command. No lengthy explanations.

---

## feature-spec

**Purpose:** Detailed specification for a single feature.

**Required Sections:**

```markdown
# Feature: [Name]

## Overview
What this feature does and why. One paragraph.

## User Stories
[TABLE: story ID | as a... | I want... | so that... | priority]

## Detailed Behavior
For each behavior:
### [Behavior Name]
**Trigger:** What causes this behavior.
**Process:**
[DIAGRAM: mermaid flowchart — decision/behavior flow]
**Output:** What the user sees.

## UI Specifications
If applicable.
[TABLE: element | type | behavior | validation | error message]

## Edge Cases
[TABLE: scenario | expected behavior | error message if applicable]

## Dependencies
[TABLE: dependency | type | version | purpose]
```

---

## project-brief

**Purpose:** One-page project definition. Goals, scope, stakeholders, success criteria.

**Required Sections:**

```markdown
# [Project Name] Brief

## Problem
What problem are we solving? Evidence that it's a real problem.

## Solution
High-level approach. 2-3 sentences.

## Success Criteria
[TABLE: metric | target | measurement method | deadline]

## Scope
[TABLE: in scope | out of scope]

## Stakeholders
[TABLE: name/role | responsibility | decision authority]

## Timeline
[TABLE: milestone | target date | deliverable]

## Risks
[TABLE: risk | probability | impact | mitigation]
```

---

## howto-guide

**Purpose:** Step-by-step instructions for a specific task.

**Required Sections:**

```markdown
# How to [Task]

## When to Use
Situations where this guide applies.

## Prerequisites
[TABLE: requirement | details]

## Steps
[DIAGRAM: mermaid flowchart — overall process overview]

### Step 1: [Action]
[Instructions with code blocks if needed]
Expected: [result]

### Step 2: [Action]
...

## Troubleshooting
[TABLE: problem | cause | fix]

## Related Guides
Links to related documentation.
```

---

## ops-manual

**Purpose:** Runbook for operating the system. Monitoring, alerts, escalation.

**Required Sections:**

```markdown
# Operations Manual: [Service Name]

## System Overview
[DIAGRAM: mermaid graph — deployment topology]

## Monitoring
[TABLE: metric | dashboard | alert threshold | normal range]

## Alert Response
For each alert:
### [Alert Name]
**Severity:** P0/P1/P2/P3
**Symptoms:** What the user experiences.
**Diagnosis:**
[DIAGRAM: mermaid flowchart — diagnostic decision tree]
**Resolution:**
Numbered steps.

## Escalation Path
[TABLE: severity | response time | contact | escalation trigger]

## Common Procedures
[TABLE: procedure | frequency | steps reference | rollback]

## Backup & Recovery
[TABLE: data | backup frequency | retention | recovery time | recovery steps]
```

---

## faq

**Purpose:** Common problems and solutions.

**Required Sections:**

```markdown
# FAQ

## [Category 1]
### Q: [Question in user's words]
A: [Direct answer. 1-3 sentences. Link to detailed docs if needed.]

### Q: [Question]
A: [Answer]

## [Category 2]
...
```

**Format Rules:**
- Questions in the user's words, not technical jargon
- Answers are 1-3 sentences with links to detail
- Group by category
- Most common questions first

---

## handover

**Purpose:** Knowledge transfer for new team members or clients.

**Required Sections:**

```markdown
# Handover: [Project/System Name]

## Project Overview
What this is, who uses it, key contacts.

## Access & Credentials
[TABLE: resource | URL | access method | contact for permissions]
(Do NOT include actual passwords. Link to secrets manager.)

## Architecture
[DIAGRAM: mermaid graph — system overview]
Link to full architecture doc.

## Current Status
[TABLE: workstream | status | owner | next steps | deadline]

## Known Issues
[TABLE: issue | severity | workaround | fix timeline]

## Key Decisions Log
[TABLE: decision | date | rationale | ADR link]

## Outstanding Tasks
[TABLE: task | priority | context | estimated effort]
```
