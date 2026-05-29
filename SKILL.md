---
name: spec-compliance-audit
description: Audits a local or remote repository/directory against a project specification (PRD, feature list, wireframe description, markdown spec, PDF, or text description) to determine compliance, identify missing features, find gaps, and produce a clear orientation report + concrete roadmap of next steps for a coding agent to execute. Make sure to use this skill whenever the user wants to compare a specification or list of requirements against a codebase, check what is built vs what is missing, orient an agent for subsequent development tasks, or conduct a feature gap analysis.
---

# Spec Compliance Audit Skill (Optimized)

Use this skill to automate the audit loop comparing a project specification (PRD, wireframe description, epic requirements, or markdown spec) against a target directory, codebase, or repository. 

This skill is highly optimized for **agentic precision, actionable planning, and instant developer orientation**. It guides the agent to bypass "optimism bias," map system architecture, and generate a step-by-step developer playbook that subsequent runs can execute without ambiguity.

---

## The Agentic Audit Workflow

Follow these four phases sequentially and exhaustively. 

```
┌─────────────────────────────────┐      ┌─────────────────────────────────┐
│     Phase 1: Deconstruct        │ ───> │        Phase 2: Map & Map       │
│ Extract atomic requirements.    │      │ Locate file references, trace   │
│ Define verification criteria.   │      │ entry points & architectures.   │
└─────────────────────────────────┘      └─────────────────────────────────┘
                 │                                        │
                 ▼                                        ▼
┌─────────────────────────────────┐      ┌─────────────────────────────────┐
│     Phase 3: Rigorous Grade     │ ───> │     Phase 4: Playbook Roadmap   │
│ Check logic, edge cases & errors.│      │ Draft detailed, self-contained  │
│ Assign FC / PC / NC / DV.       │      │ tasks with exact stubs & DoD.   │
└─────────────────────────────────┘      └─────────────────────────────────┘
```

### Phase 1: Parse, Deconstruct, & Establish Criteria
1. Locate and read the project specification. 
2. Break down the spec into atomic, granular requirements. Do not lump multiple features together.
3. Assign a unique requirement ID to each item (e.g., `REQ-FUN-001`, `REQ-UI-002`, `REQ-NFN-003`).
4. **Define Verification Criteria**: For each requirement, establish what constitutes "Fully Compliant" (e.g., "Must have database column X, validation of field Y, and return error code Z on failure").

### Phase 2: Architectural Mapping & Exploration
1. Walk the directory tree to inspect the codebase framework, routing mechanisms, database configurations, and core dependencies.
2. Identify and document:
   - **Main Entry Points & Routers**: Where requests enter or pages load.
   - **State & Context Management**: Libraries used (e.g., Redux, Zustand, React Context) to prevent redundant library insertion.
   - **Styling Conventions**: CSS frameworks, Tailwind versions, custom components.
   - **Database Schemas**: Models, migrations, or data tables.

### Phase 3: Rigorous Compliance Grading (Anti-Optimism Protocol)
Do not grade a requirement as Fully Compliant (`[FC]`) purely by filename association or because a simple function exists. You must verify:
- **Core Business Logic**: The logic matches the spec's formulas, rules, and outcomes.
- **Edge-Case Validation**: Correctly handles empty inputs, nulls, invalid formats, or missing privileges.
- **Graceful Error Handling**: Appropriate try/catch blocks, human-readable error messages, and API error codes.

**Grades**:
* `[FC]` **Fully Compliant**: Meets all core logic, edge-case, and error requirements.
* `[PC]` **Partially Compliant**: Core logic is present, but lacks edge cases, error handling, visual styling, or integration.
* `[NC]` **Non-Compliant/Missing**: No trace of this requirement is found in the codebase.
* `[DV]` **Divergent/Out-of-Spec**: Built differently than the spec requested. Provide the technical rationale (e.g., "Using SQLite instead of PostgreSQL due to local environment constraints").

### Phase 4: Constructing the Actionable Playbook (Next Steps)
Convert all `PC`, `NC`, and `DV` requirements into a prioritized implementation roadmap designed for a coding agent to execute seamlessly:
1. **Group by Context**: Arrange tasks logically to minimize context-switching (e.g., group all database migrations and backend models together before frontend integration).
2. **Provide Definition of Done (DoD)**: Write exact criteria to verify each task's completion.
3. **Include Technical Stubs**: Include stubs, API routes, or code patterns so the next agent doesn't have to design interfaces from scratch.

---

## Output Template

Your final output must be saved to a file named `spec_audit_report.md` in the root of the audited repository (or workspace) AND summarized clearly in your response. The report MUST use the following exact structure:

```markdown
# Spec Compliance Audit Report

## 1. Executive Summary
- **Audit Target**: [Target directory or repository]
- **Specification Source**: [Spec file name or source]
- **Overall Completion Rate**: [Calculated as: (FC / Total Requirements) * 100]%
- **Summary Metrics**:
  - **Total Requirements**: [X]
  - **Fully Compliant (FC)**: [A]
  - **Partially Compliant (PC)**: [B]
  - **Non-Compliant/Missing (NC)**: [C]
  - **Divergent (DV)**: [D]

### High-Level Review
[A 2-3 paragraph summary of the general codebase health, architectural consistency, and quality. Highlight major accomplishments and pinpoint the single largest blocker to 100% spec compliance.]

---

## 2. Architectural Blueprint & Constraints Map
- **Core Tech Stack**: [Languages, frameworks, database system]
- **Primary Dependencies**: [List key state management, auth, or styling libraries in use]
- **Key Architectural Entry Points**:
  - **Router / Router Files**: [Absolute file path link]
  - **Main Controller / Logic Root**: [Absolute file path link]
- **Development Constraints**: [Note database constraints, custom lint rules, UI design systems, or strict conventions in the codebase]

---

## 3. Compliance Matrix
| Req ID | Category | Requirement Description | Status | Implementation File Reference & Evidence / Gaps |
| :--- | :--- | :--- | :--- | :--- |
| REQ-FUN-001 | Functional | Implement secure JWT-based login | `FC` | [src/controllers/authController.ts](file:///absolute/path/to/src/controllers/authController.ts#L22-L58) - Full validation and error routing verified. |
| REQ-UI-002 | UI/UX | Display validation errors in login form | `PC` | [src/components/LoginForm.tsx](file:///absolute/path/to/src/components/LoginForm.tsx#L45-L72) - Form displays empty fields but misses invalid email formatting warning. |
| REQ-FUN-003 | Functional | OAuth Google login capability | `NC` | *None* - Entirely missing. |

*Statuses: `FC` (Fully Compliant), `PC` (Partially Compliant), `NC` (Non-Compliant/Missing), `DV` (Divergent)*

---

## 4. Detailed Gap Analysis
[For every `PC`, `NC`, and `DV` requirement, provide a granular breakdown of exactly what is missing, broken, or misaligned, and reference the specific files involved.]

### [Req ID] - [Requirement Name]
* **Current State**: [Describe the current partial implementation, divergence, or total absence]
* **Verification Gaps**:
  - [ ] [Gap description, e.g., Missing try/catch and error response for database timeouts]
  - [ ] [Gap description, e.g., Input schema does not filter out malicious HTML]
* **Technical Guidance**: [A brief developer instruction on how to build/fix this gap]

---

## 5. Oriented Developer Playbook (Roadmap)
[A prioritized, logical sequence of actions that can be fed directly to the next coding agent run to achieve 100% compliance.]

### Phase A: Database & Backend Foundations
1. **[Task Name]**
   - **Target Files**: [List absolute file paths]
   - **Action**: [Clear step-by-step description of what to implement]
   - **Technical Details / Interface Stub**:
     ```typescript
     // Provide code interfaces, routing stubs, or database schemas here
     ```
   - **Definition of Done (DoD)**:
     - [ ] Verification requirement A (e.g., API returns 201 Created on valid POST)
     - [ ] Verification requirement B (e.g., Migration file created and run successfully)

### Phase B: Core Logic & Integration
...

### Phase C: UI/UX & Aesthetics Polish
...
```

---

## Critical Execution Guidelines for the Agent
1. **Rigorous Inspection over Assumption**: Do not assume a requirement is met just because a file or class has a matching name. View the file and check for actual logic, edge cases, and error handling.
2. **Be Visual & Aesthetic Aware**: If the project spec details visual mockups, styles, colors, or animations, inspect the CSS or stylesheet code. Note any raw/unpolished UI elements under the Divergent (`DV`) or Partially Compliant (`PC`) categories.
3. **Hyperlink Files**: Always use absolute `file:///` URLs when referring to files so the user or next agent can jump straight to the source code. Include line ranges if applicable.
