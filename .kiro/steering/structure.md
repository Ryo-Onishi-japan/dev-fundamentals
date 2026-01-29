# Project Structure Steering

## Root Directory Organization

The root directory of this repository is organized to provide clear access to documentation, configuration, and development assets.

-   `docs/`: Contains all project documentation and learning guides.
-   `java/`: Contains the Java source code for the "employee management system" tutorial.
-   `sql/`: Contains the PL/SQL scripts for the tutorial.
-   `.env.example`, `.envrc`: Environment variable examples and configuration.
-   `.gitignore`: Specifies intentionally untracked files to ignore.
-   `README.md`: Primary project overview and entry point.
-   `GEMINI.md`: AI Development Life Cycle (AI-DLC) and Kiro-style Spec Driven Development documentation.
-   `setup.sh`: Script for initial environment setup.
-   `.gemini/`: Configuration and commands for the Gemini CLI.
-   `.git/`: Git version control system files.
-   `.kiro/`: Kiro-style Spec Driven Development configuration and steering/specification files.

## Kiro-Style Spec Driven Development (`.kiro/`)

This directory is central to the Kiro-style Spec Driven Development process.

-   `.kiro/settings/`: Contains templates and rules for steering and specifications.
    -   `.kiro/settings/rules/`: Defines principles and guidelines (e.g., `steering-principles.md`).
    -   `.kiro/settings/templates/`: Provides templates for generating various project documents (e.g., steering files).
-   `.kiro/steering/`: Contains project-wide rules and context that guide AI development. These files (e.g., `product.md`, `tech.md`, `structure.md`) serve as persistent project memory.
-   `.kiro/specs/`: Will contain formal specifications for individual features as development progresses.

## General Principles

-   **Separation of Concerns:** The project is organized by technology, with dedicated directories for documentation (`docs/`), Java code (`java/`), and SQL scripts (`sql/`).
-   **Configuration Grouping:** Tool-specific configurations (e.g., `.gemini/`, `.kiro/`) are grouped within their respective hidden directories.
-   **Centralized Documentation:** All learning materials are centralized in the `docs/` directory for easy access.
