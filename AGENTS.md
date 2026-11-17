
# Codex Instructions — LumiLearn

## 1. Project Context

LumiLearn is an educational application designed to help parents assess and improve their children's reading comprehension.

The application allows parents to:

- Register and manage student profiles.
- Upload textbook pages progressively.
- Extract all visible text or only highlighted text from images.
- Review, correct, and confirm extracted text.
- Consolidate text from multiple pages into a single study document.
- Generate comprehension questions using OpenAI.
- Review, edit, and approve generated questionnaires.
- Assign questionnaires to students.
- Review AI-proposed assessments and approve final grades.
- Generate additional questionnaires based on previous mistakes.
- Track student progress and preserve learning history.

The application must support incremental development and future extensibility.

## 2. Sources of Truth

Before starting any development task, read the following files:

1. `docs/requirements.md`
   Functional requirements, business rules, and acceptance criteria.

2. `docs/architecture.md`
   Application architecture, responsibilities, and technical boundaries.

3. `docs/stack.md`
   Approved or proposed technologies and development tools.

4. `docs/implementation-plan.md`
   Development phases, dependencies, and implementation progress.

5. `README.md`
   Project overview and general instructions.

If any documentation contains contradictions, missing information, or unresolved decisions, ask for clarification before proceeding.

Do not invent requirements or assume that pending decisions have been approved.

## 3. Development Workflow

Development must follow an incremental and requirements-driven approach.

### Step 1: Analyze

Before implementing a requirement:

- Read the corresponding functional requirement.
- Identify all acceptance criteria.
- Identify dependencies on other requirements.
- Review the proposed architecture.
- Identify affected components and files.
- Identify technical risks and unresolved decisions.

### Step 2: Plan

Prepare an implementation plan containing:

- Requirement identifier and objective.
- Scope of the implementation.
- Proposed technical approach.
- Files to create or modify.
- Dependencies.
- Automated tests.
- Expected results.
- Potential risks.

### Step 3: Request Approval

IMPORTANT:

Do not generate code, create files, modify existing files, or install dependencies without explicit user approval.

Present the implementation plan and wait for approval.

If the user requests changes, update the plan before implementation.

### Step 4: Implement

After receiving approval:

- Implement only the approved scope.
- Follow the documented architecture.
- Apply SOLID principles.
- Keep the code modular and maintainable.
- Avoid unnecessary complexity.
- Do not implement unrelated requirements.
- Do not introduce dependencies without justification.

### Step 5: Test

After implementation:

- Create automated tests for the implemented functionality.
- Verify the relevant acceptance criteria.
- Test error handling and edge cases.
- Execute the available tests.
- Report any tests that could not be executed.

### Step 6: Report

After completing an increment, provide:

- Requirement implemented.
- Acceptance criteria covered.
- Files created or modified.
- Tests executed and results.
- Technical decisions made.
- Known limitations.
- Recommended next increment.

Wait for user approval before continuing.

## 4. Architecture Rules

The application must follow the architecture described in `docs/architecture.md`.

General principles:

- Apply Clean Architecture.
- Follow SOLID principles.
- Separate business logic from infrastructure.
- Keep domain entities independent of frameworks.
- Use dependency inversion when integrating external services.
- Separate controllers, use cases, repositories, and external services.
- Avoid unnecessary coupling between modules.
- Keep frontend and backend responsibilities separate.

Domain logic must not depend directly on:

- Express.
- Database ORM implementations.
- OpenAI SDK.
- External infrastructure services.

External integrations must be accessed through clearly defined interfaces.

## 5. Backend Rules

Follow the technologies approved in `docs/stack.md`.

General guidelines:

- Use TypeScript.
- Expose functionality through REST APIs.
- Validate incoming requests.
- Implement consistent error handling.
- Keep API routes and controllers lightweight.
- Place business logic in application use cases.
- Use repositories for data persistence.
- Keep secrets in environment variables.
- Never expose OpenAI API keys to the frontend.

Do not introduce new frameworks or libraries without justification and approval.

## 6. Frontend Rules

Follow the frontend technologies documented in `docs/stack.md`.

General guidelines:

- Use reusable components.
- Separate presentation logic from API communication.
- Implement clear loading, success, and error states.
- Validate user input.
- Provide understandable feedback to parents and students.
- Keep the user interface accessible and maintainable.

## 7. OpenAI Integration Rules

OpenAI is used to support:

- Text extraction from textbook images.
- Detection and extraction of highlighted text.
- Generation of comprehension questions.
- Generation of reference answers.
- Provisional assessment of student responses.
- Generation of additional practice questions.

Rules:

- OpenAI integration must remain in the backend.
- Do not expose API keys.
- Handle API errors and timeouts.
- Avoid unnecessary API calls.
- Do not invent text when image content is unreadable.
- Preserve the original extraction results when appropriate.
- Allow parents to review and correct extracted content.
- Do not treat AI-generated assessments as final grades.

Final student assessments require parental approval.

## 8. Progressive Document Processing

LumiLearn supports progressive image processing.

A study document may contain multiple textbook pages.

Rules:

- Each uploaded image belongs to a study document.
- Each page must preserve its own extracted text.
- Each page must preserve its extraction mode.
- Parents may add pages at different times.
- Previously processed pages must not be reprocessed unnecessarily.
- Parents must be able to review and correct each page.
- The consolidated text must respect page order.
- Adding or modifying a page must update the consolidated content.
- A document can be confirmed only when all its pages have been reviewed.
- Quiz generation must use confirmed document content.

Existing quizzes and student attempts must remain associated with the source-text version used when they were created.

## 9. Security and Privacy

LumiLearn processes information related to children.

Security and privacy must be considered throughout development.

Rules:

- Never commit secrets or API keys.
- Never log passwords or authentication tokens.
- Avoid logging children's personal information.
- Validate uploaded files.
- Enforce authorization when accessing resources.
- Apply secure password storage practices.
- Minimize personal data collection.
- Protect student responses and assessment history.
- Do not expose internal errors or sensitive infrastructure details.

## 10. Testing Requirements

Every implemented requirement must include appropriate tests.

Tests should cover:

- Expected behavior.
- Relevant acceptance criteria.
- Invalid inputs.
- Error handling.
- Important edge cases.
- Data persistence when applicable.

Use mocks or test doubles for external services when appropriate.

Do not make real OpenAI API calls in ordinary unit tests.

Report test execution results after each implementation.

## 11. Documentation Rules

Keep documentation consistent with the implementation.

When necessary:

- Update `docs/implementation-plan.md`.
- Document important architectural decisions.
- Record unresolved questions.
- Identify incomplete acceptance criteria.
- Explain deviations from the original plan.

Do not mark a requirement as completed unless its acceptance criteria have been verified.

## 12. Git Rules

Use clear and descriptive commit messages.

Follow Conventional Commits when appropriate.

Examples:

- `chore: initialize project structure`
- `docs: update functional requirements`
- `feat: implement text extraction`
- `test: add text extraction unit tests`
- `fix: handle OpenAI extraction errors`
- `refactor: separate extraction use case`

Do not create commits or push changes without explicit user approval.

## 13. Current Development Priority

The initial development priority is:

**RF-004: Progressive Text Extraction**

RF-004 may be implemented before RF-001 and RF-003.

To support this approach:

- Use local test images.
- Use temporary test document identifiers.
- Avoid implementing authentication prematurely.
- Avoid implementing the complete image upload interface.
- Keep temporary solutions isolated and replaceable.

Suggested increments:

1. Extract all readable text from one local image.
2. Extract highlighted text from one local image.
3. Process multiple images progressively.
4. Consolidate extracted text in page order.
5. Persist extracted text and extraction metadata.

These increments are implementation steps, not new functional requirements.

## 14. Mandatory Approval Rule

Before starting any implementation:

1. Read the project documentation.
2. Analyze the requested requirement.
3. Present a proposed implementation plan.
4. Identify dependencies and tests.
5. Wait for explicit user approval.

Do not start coding until approval is received.

After completing an approved increment, stop and report the results.

Do not automatically proceed to the next increment.

The user maintains final control over implementation decisions.
