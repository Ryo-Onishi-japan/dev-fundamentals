# Requirements Document

## Project Description (Input)
I want to create a tutorial for 'monozukuri' (manufacturing/making things) that is not an employee management system.

## Introduction
This document outlines the requirements for a hands-on tutorial designed to teach foundational developer skills through the creation of a 'monozukuri' (making things) themed application. The tutorial aims to provide practical experience in GitHub workflows, Java programming, PL/SQL database interactions, and AI-driven coding practices, excluding the domain of employee management systems.

## Requirements

### 1. Tutorial Project Management
**Objective:** As a developer, I want a structured tutorial environment, so that I can learn foundational development skills.

#### Acceptance Criteria
1.  When a developer follows the tutorial, the learning environment shall provide clear steps for setting up a development environment.
2.  The tutorial shall guide the developer through basic GitHub workflows, including branching, committing, and pull requests.
3.  The tutorial shall incorporate AI-driven coding practices using the Gemini CLI and Kiro-style Spec-Driven Development.

### 2. Monozukuri Application Core Functionality
**Objective:** As a user, I want to manage aspects of a 'monozukuri' project, so that I can track progress and resources.

#### Acceptance Criteria
1.  The system shall allow users to register and view details of various 'monozukuri' projects (e.g., project name, description, status).
2.  The system shall allow users to manage a list of materials required for each project, including material name, quantity, and unit.
3.  The system shall allow users to mark projects as completed or in progress.

### 3. Data Persistence
**Objective:** As a system, I want to securely store and retrieve 'monozukuri' project data, so that user information is persistent across sessions.

#### Acceptance Criteria
1.  The Java application shall interact with a PL/SQL database to store project and material data.
2.  The PL/SQL database shall maintain data integrity for project and material information.

### 4. User Interface
**Objective:** As a user, I want to interact with the 'monozukuri' application through a simple interface, so that I can easily manage projects and materials.

#### Acceptance Criteria
1.  The system shall provide a user-friendly interface for creating, viewing, and updating projects.
2.  The system shall provide a user-friendly interface for adding and listing materials for a given project.