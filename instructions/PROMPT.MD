## Genarating Copilot Instructions

prompt:
``` markdown
I want you to generate a comprehensive `instructions.md` file in .github folder that will serve as your primary rulebook for this project. 
**The core requirement for this task, and for all your future interactions with this project, is absolute precision, logical order, and technical accuracy.**
please follow these steps:
### Step 1: Project Analysis
Analyze the current workspace and identify:
1. The Tech Stack: Detect versions of frameworks (e.g., .NET version, required pkgs, versions).
2. Architecture: Identify the design patterns used (e.g., Clean Architecture, Onion, Layered, Repository Pattern).
### Step 2: File Generation
Based on your findings, write the instructions.md file with the following sections:
- Project Overview & Goals: A brief summary of what this system does.
- Technical Stack: A list of all languages, frameworks, and versions.
- Architectural Rules: Explicit instructions on where to put new logic (e.g., 'Models' for entities, 'Services' for bussines logic).
- Coding Standards: Guidelines for naming conventions, file structure, and typing (e.g., CamelCase in functions naming).
- Self-Correction Clause: Add a rule that you must verify every suggestion against this file before responding.

### Step 3: Modular Documentation & Implementation Standards
Please modularize the instructions to ensure maximum clarity and maintainability. Follow these specific requirements:

**1.  File Separation (Modular Rules):**

- Create a dedicated section (or separate files if the environment allows) for Controllers and Services.

- Controllers Module: Define the standards for API design, including Route naming conventions, HTTP verb usage, DTO validation, and Response wrapping.

- Services Module: Define the standards for Business Logic encapsulation, Dependency Injection, and the separation of concerns between the Service layer and Data Access.

2. Cross-Referencing:
In the main instructions.md, provide high-level summaries. Include explicit "See More" references or links pointing to the detailed Controller/Service modules for deep-dive technical rules.


```