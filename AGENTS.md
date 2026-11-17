
# LumiLearn — Codex Instructions

## 1. Project Context

LumiLearn is an educational application that helps parents
improve their children's reading comprehension through
AI-assisted document processing, quizzes, and assessments.

## 2. Project Documentation

Use these files as the source of truth:

- `docs/requirements.md` — Functional requirements and
  acceptance criteria.
- `docs/architecture.md` — Architecture and design rules.
- `docs/stack.md` — Technology stack.
- `docs/implementation-plan.md` — Development phases
  and progress.
- `README.md` — Project overview.

Read the relevant documentation before each task.
If requirements conflict or decisions are missing,
ask for clarification. Never invent requirements.

## 3. Development Workflow

Follow this workflow for every implementation:

1. **Analyze:** Identify the requirement, acceptance
   criteria, dependencies, and affected components.
2. **Plan:** Propose implementation steps, affected
   files, risks, and required tests.
3. **Approve:** Wait for explicit user approval before
   creating or modifying files, generating code,
   or installing dependencies.
4. **Implement:** Execute only the approved scope,
   one small increment at a time.
5. **Test:** Run relevant automated tests and verify
   acceptance criteria.
6. **Report:** Summarize changes, test results,
   limitations, and the next proposed increment.

Never proceed to another increment without approval.

## 4. Architecture and Code Quality

- Follow Clean Architecture and SOLID principles.
- Respect `docs/architecture.md` and `docs/stack.md`.
- Keep domain logic independent of frameworks,
  databases, and external services.
- Separate controllers, use cases, repositories,
  and infrastructure integrations.
- Use TypeScript and maintain modular, testable code.
- Avoid unnecessary dependencies and complexity.
- Do not implement unapproved features.

## 5. Security and AI

- Keep API keys and secrets in environment variables.
- Never expose secrets or sensitive student information.
- Validate inputs, uploads, and resource access.
- Keep OpenAI integrations on the backend.
- Handle external API failures.
- Do not invent unreadable extracted text.
- Require parental approval for final AI-assisted grades.
- Preserve previous quizzes, attempts, and their
  original source-text versions.

## 6. Testing and Documentation

- Add tests for implemented acceptance criteria.
- Mock external services in unit tests.
- Report tests that could not be executed.
- Update `docs/implementation-plan.md` when approved.
- Never mark incomplete requirements as completed.
- Do not commit or push changes without approval.

## 7. Current Development Priority

Start with RF-004: Progressive Text Extraction.

- Use local test images until RF-003 is implemented.
- Keep temporary test data isolated and replaceable.
- Implement one small increment at a time.
- Do not implement RF-001 or RF-003 prematurely.

Always present the plan and wait for approval
before writing code.
