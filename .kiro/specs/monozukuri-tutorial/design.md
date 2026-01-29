# Design Document Template

---
**Purpose**: Provide sufficient detail to ensure implementation consistency across different implementers, preventing interpretation drift.

**Approach**:
- Include essential sections that directly inform implementation decisions
- Omit optional sections unless critical to preventing implementation errors
- Match detail level to feature complexity
- Use diagrams and tables over lengthy prose

**Warning**: Approaching 1000 lines indicates excessive feature complexity that may require design simplification.
---

> Sections may be reordered (e.g., surfacing Requirements Traceability earlier or moving Data Models nearer Architecture) when it improves clarity. Within each section, keep the flow **Summary → Scope → Decisions → Impacts/Risks** so reviewers can scan consistently.

## Overview
**Purpose**: This feature delivers a hands-on tutorial for foundational developer skills through the creation of a 'monozukuri' (making things) themed application.
**Users**: Developers new to the workforce, students learning software development, and individuals practicing skills in Java, PL/SQL, GitHub, and AI-driven coding.
**Impact**: Provides a practical, non-employee management system example to teach core development concepts, aligning with the project's learning objectives.

### Goals
- Provide a structured tutorial for developing a "Crafting Project Tracker".
- Teach GitHub workflows, Java programming, and PL/SQL database interactions.
- Demonstrate AI-driven coding practices using the Gemini CLI and Kiro-style Spec-Driven Development.
- Offer a practical application example that is distinct from an employee management system.

### Non-Goals
- Building a production-ready "Crafting Project Tracker" with advanced features (e.g., user authentication, complex reporting).
- Comprehensive coverage of all aspects of Java or PL/SQL beyond foundational concepts relevant to the tutorial.
- Providing a tutorial for any specific frontend framework (focus on backend/database/workflow).

## Architecture

### Existing Architecture Analysis (if applicable)
The project steering (`structure.md`, `tech.md`) emphasizes modularity, separation of concerns, and spec-driven development. The current setup supports Java for application logic and PL/SQL for database interaction. This design will adhere to these established patterns.

### Architecture Pattern & Boundary Map


```mermaid
graph TD
    UserInterface[User Interface] --> JavaApplication[Java Application (Backend)]
    JavaApplication --> PLSQLDatabase[PL/SQL Database]
```

**Architecture Integration**:
- Selected pattern: Client-Server Architecture. This pattern is well-understood and suitable for teaching foundational development skills.
- Domain/feature boundaries: The Java Application will handle business logic for Project and Material management. The PL/SQL Database will manage data persistence and integrity. The User Interface (implicitly a simple web UI for the tutorial) will interact with the Java Application's APIs.
- Existing patterns preserved: Adheres to the separation of concerns between application logic (Java) and database logic (PL/SQL) as outlined in `tech.md`.
- New components rationale: The "Java Application (Backend)" and "PL/SQL Database" are integral to the tutorial's technical scope.
- Steering compliance: Aligns with the modularity and technology stack principles from `tech.md` and `structure.md`.

### Technology Stack

| Layer | Choice / Version | Role in Feature | Notes |
|---|---|---|---|
| Frontend / CLI | (Implicit simple web UI) | Interaction with Java Application APIs | Tutorial focuses on backend, database, and workflow. |
| Backend / Services | Java | Business logic for projects and materials | Handles API endpoints, data processing. |
| Data / Storage | PL/SQL Database | Persistent storage of project and material data | Ensures data integrity and transactional operations. |
| Messaging / Events | N/A | Not required for foundational tutorial | |
| Infrastructure / Runtime | JVM, Oracle Database (or compatible) | Execution environment and data store | Tutorial assumes a local development setup for these. |

## System Flows
This tutorial features straightforward CRUD operations, so a complex system flow diagram is not strictly necessary at this stage. The primary flow involves:
1. User interacts with UI to create/read/update/delete Project or Material.
2. UI calls corresponding API in Java Application.
3. Java Application performs business logic, interacts with PL/SQL Database.
4. PL/SQL Database stores/retrieves data.
5. Java Application returns response to UI.

## Requirements Traceability
For this foundational tutorial, direct traceability from requirements to components is sufficient without an explicit table here. Each requirement generally maps to a set of CRUD operations on either `Project` or `Material` entities handled by the Java Application and stored in the PL/SQL Database.

## Components and Interfaces

### Java Application (Backend)
- **Responsibility**: Expose RESTful APIs for managing 'Crafting Projects' and 'Materials'. Implement business logic for data validation and processing.
- **Interfaces**:
    - **Project API**:
        - `POST /projects`: Create a new crafting project.
        - `GET /projects`: Retrieve all crafting projects.
        - `GET /projects/{id}`: Retrieve a specific crafting project by ID.
        - `PUT /projects/{id}`: Update an existing crafting project.
        - `DELETE /projects/{id}`: Delete a crafting project.
    - **Material API**:
        - `POST /projects/{projectId}/materials`: Add a new material to a project.
        - `GET /projects/{projectId}/materials`: Retrieve all materials for a project.
        - `GET /projects/{projectId}/materials/{id}`: Retrieve a specific material by ID within a project.
        - `PUT /projects/{projectId}/materials/{id}`: Update an existing material within a project.
        - `DELETE /projects/{projectId}/materials/{id}`: Delete a material from a project.
- **Data Structures (High-Level)**:
    - `Project`: ID (UUID), Name (String), Description (String), Status (Enum: Planned, In Progress, Completed).
    - `Material`: ID (UUID), Project ID (UUID), Name (String), Quantity (Number), Unit (String).

### PL/SQL Database
- **Responsibility**: Persist and manage 'Crafting Project' and 'Material' data. Ensure data integrity through relationships and constraints.
- **Interfaces**: Accessed by the Java Application via JDBC (or similar database connector).
- **Schema (High-Level)**:
    - `PROJECTS` table: `ID` (PK), `NAME`, `DESCRIPTION`, `STATUS`.
    - `MATERIALS` table: `ID` (PK), `PROJECT_ID` (FK to PROJECTS.ID), `NAME`, `QUANTITY`, `UNIT`.
- **Stored Procedures/Functions**: Simple CRUD operations potentially encapsulated in basic stored procedures for the tutorial.