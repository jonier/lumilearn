# Incremental implementation plan — LumiLearn

**Status:** Proposed plan; no phase marked as complete.

## Working method
For each phase: review acceptance criteria → propose design and tests → obtain approval → implement a small task → run tests → review code → update this plan → continue. Do not ask Codex to implement the entire application at once.

## Phase 0 — Preparation
- [ ] Approve requirements and pending decisions that block the relevant phase.
- [ ] Approve the stack and architecture.
- [ ] Initialize Git and the frontend/backend structure.
- [ ] Configure TypeScript, validation, linting, and tests.
- [ ] Create a `/health` endpoint and verify the frontend-backend connection.
- [ ] Configure example environment variables without real secrets.

## Phase 1 — RF-001 and RF-002: accounts and students
- [ ] Registration/login/logout and authorization.
- [ ] Basic CRUD for child profiles.
- [ ] Account-isolation tests.

## Phase 2 — RF-003: documents and progressive pages
- [ ] Create a document with a title.
- [ ] Upload one image and add others at different times.
- [ ] List, reorder, and delete pages.
- [ ] File persistence and validation.
- [ ] Tests ensuring previous pages are not lost.

## Phase 3 — RF-004: page extraction
- [ ] `TextExtractor` interface and AI adapter.
- [ ] Select full or highlighted mode for each page.
- [ ] Save each page's extraction and mode.
- [ ] Retries and failures without overwriting other pages.
- [ ] Ordered consolidated view.
- [ ] Tests with a mocked AI provider.

## Phase 4 — RF-005: correction and confirmation
- [ ] Edit/save/confirm text for each page.
- [ ] Show pending pages.
- [ ] Confirm the document only when all pages have been reviewed.
- [ ] Create an immutable snapshot of the consolidated text.
- [ ] Invalidate the current confirmation when pages change without affecting previous versions.
- [ ] Persistence and reconstruction tests.

## Phase 5 — RF-006 and RF-007: generation and approval
- [ ] Generate questions/answers from a confirmed version.
- [ ] Review, edit, delete, and regenerate questions.
- [ ] Approve the quiz and preserve its source.
- [ ] Tests for AI errors and authorization.

## Phase 6 — RF-008 and RF-009: assignment and answers
- [ ] Approve the student's access model.
- [ ] Assign approved quizzes.
- [ ] Allow students to answer and submit attempts.
- [ ] Persist answers and dates.

## Phase 7 — RF-010: mixed evaluation
- [ ] Propose grades and explanations with AI.
- [ ] Show answers and references to the parent.
- [ ] Allow grades and notes to be edited.
- [ ] Approve the final evaluation while preserving the original proposal.
- [ ] Tests requiring approval.

## Phase 8 — RF-011 and RF-012: reinforcement and history
- [ ] Generate new questions about the same content.
- [ ] Design the question bank and reuse rules.
- [ ] Prioritize missed concepts when sufficient data exists.
- [ ] Compare attempts and display progress.
- [ ] Keep previous evaluations and versions unchanged.

## Phase 9 — End-to-end validation and deployment
- [ ] E2E tests: 5–10 pages added progressively, mixed extraction, corrections, quiz, answers, approved evaluation, and repetition.
- [ ] Verify persistence after restart.
- [ ] Review security, privacy, accessibility, and AI costs.
- [ ] Prepare deployment and operational documentation.

## Known blockers
- Question types, child access, grading scale, languages, data policy, upload limits, and question-bank rules.
- The phase order is a proposal; work may begin with a vertical slice of RF-003 through RF-005 using simulated authentication **in development only**, but it must not be exposed as a secure product.

## First suggested prompt for Codex

> Read `AGENTS.md`, `README.md`, and the four documents in `docs/`. Check consistency, dependencies, and pending decisions. Propose only a detailed plan for Phase 0. Do not write code or modify files yet. Identify risks and wait for my approval.
