# Architecture — LumiLearn proposal

**Status:** Initial design pending approval. Client-server architecture, REST API, and modular monolith using Clean Architecture by feature.

## 1. Overview

```text
[React Frontend]
       |
       | HTTPS / REST / session cookies
       v
[Express Backend — Presentation layer]
       |
       v
[Application: use cases + ports]
       |
       v
[Domain: entities + rules]
       ^
       |
[Infrastructure: SQL, private files, AI provider]
```

Domain dependencies point inward: neither the domain nor the use cases import Express, Sequelize, or the OpenAI SDK. Infrastructure implements interfaces defined by the inner layers.

## 2. Suggested functional modules
- `auth`: registration, sessions, authorization.
- `students`: child profiles.
- `documents`: documents, pages, ordering, extracted/corrected text, confirmation, and versions.
- `questions`: question bank, generation, and approval.
- `quizzes`: quizzes, assignments, and attempts.
- `evaluations`: automated proposals, parent review, and approval.
- `progress`: history and attempt comparisons.

## 3. Conceptual entities
- `ParentAccount`
- `StudentProfile`
- `StudyDocument` (title, owner, status)
- `DocumentPage` (image, position, extraction mode, extracted text, corrected text, status)
- `ConfirmedContentVersion` (immutable snapshot of consolidated content and page metadata)
- `Question` (prompt, reference answer, source)
- `Quiz` (content version, questions, approval status)
- `QuizAssignment` (student, quiz)
- `QuizAttempt` and `StudentAnswer`
- `EvaluationProposal` and `ApprovedEvaluation`

**Invariants:** pages have an explicit order; confirmation requires reviewed pages; changing pages requires new confirmation; previous quizzes retain their source version; parent approval cannot be simulated by the AI.

## 4. Document use cases
- `CreateStudyDocument`
- `AddDocumentPage`
- `ReorderDocumentPages`
- `RemoveDocumentPage`
- `ExtractPageText` (full or highlighted mode)
- `UpdatePageText`
- `ConfirmPageText`
- `ConfirmDocumentContent` (creates an immutable version)
- `GetConsolidatedDocumentText`

Consolidation must be rebuilt from corrected and ordered pages, rather than through irreversible concatenations on every upload. Adding a new page must not by itself trigger extraction of previous pages.

## 5. Learning use cases
- `GenerateQuestionsFromContentVersion`
- `ReviewAndApproveQuiz`
- `AssignQuizToStudent`
- `SubmitQuizAttempt`
- `ProposeEvaluation`
- `ReviewAndApproveEvaluation`
- `GenerateReinforcementQuiz`
- `GetStudentProgress`

## 6. Infrastructure interfaces (ports)
- `DocumentRepository`, `PageRepository`, `ContentVersionRepository`
- `ImageStorage`
- `TextExtractor` (input: image + mode; output: text/warnings)
- `QuestionGenerator`
- `EvaluationSuggester`
- `QuizRepository`, `AttemptRepository`, `EvaluationRepository`

OpenAI adapters must handle failures, timeouts, quotas, and output validation. The AI may make mistakes when recognizing highlights or evaluating answers; the parent always reviews the result.

## 7. Suggested structure

```text
frontend/
  src/
    features/
      auth/
      students/
      documents/
      quizzes/
      evaluations/
      progress/
    shared/
backend/
  src/
    features/
      documents/
        domain/
        application/
        infrastructure/
        presentation/
      auth/
      students/
      questions/
      quizzes/
      evaluations/
      progress/
    shared/
  tests/
docs/
```

## 8. Tentative REST contracts
- `POST /api/v1/documents`
- `POST /api/v1/documents/:id/pages`
- `GET /api/v1/documents/:id/pages`
- `PATCH /api/v1/documents/:id/pages/order`
- `POST /api/v1/documents/:id/pages/:pageId/extraction`
- `PATCH /api/v1/documents/:id/pages/:pageId/text`
- `POST /api/v1/documents/:id/pages/:pageId/confirm`
- `POST /api/v1/documents/:id/confirm`
- `POST /api/v1/documents/:id/questions`
- `POST /api/v1/quizzes`

These are route examples, **not approved contracts**. They should be reviewed while designing each requirement.

## 9. Security and privacy
- Owner-based authorization for every operation on resources.
- Validate the actual file type and enforce configurable limits; files must be private, not public by default.
- Keep secrets on the server; do not log images, children's answers, or keys.
- Avoid using the child's personal data in prompts unless justified by a specific need.
- Retention, deletion, backup, and CSRF protection policies remain to be defined.

## 10. Pending decisions
Child authentication, evaluation scale, question types, production SQL model, deletion policy, file limits, languages, and deployment strategy.
