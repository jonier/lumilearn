# Technology stack — proposal pending approval

## Objective
Choose technologies compatible with incremental development and separation of responsibilities. **None of the choices here imply that they are already installed or implemented.**

| Area | Proposal | Status |
|---|---|---|
| Frontend | React 19 + TypeScript + Vite | Proposal |
| UI state | Zustand when needed | Proposal |
| Internationalization | i18next (initial languages pending) | Proposal |
| Backend | Node.js + Express + TypeScript | Proposal |
| API | REST, `/api/v1` routes | Proposal |
| Validation | Zod | Proposal |
| Local database | SQLite + Sequelize | Proposal |
| Production database | PostgreSQL or MySQL | Pending |
| Image storage | Local disk in development; private external storage in production | Pending |
| Extraction / generation / evaluation | OpenAI API, called only from the backend | Proposal |
| Authentication | Sessions or JWT in an HttpOnly cookie; strategy and CSRF protection to be defined | Pending |
| Backend tests | Vitest + Supertest | Proposal |
| Frontend tests | Vitest + React Testing Library | Proposal |
| E2E | Playwright | Proposal |
| Quality | ESLint + Prettier | Proposal |
| Tools | Git, VS Code, Codex | Planned |

## Constraints
- Never send the OpenAI key to the client.
- Avoid coupling use cases to AI providers, storage, or database technologies.
- Process each page independently; do not overwrite corrections when reprocessing other pages.
- Maintain immutable versions of confirmed text that supports quizzes.
- Protect student data and book images through authorization and private storage.

## Technical decisions to resolve
- Production storage provider and format.
- Authentication strategy and student access.
- Model and maximum cost per extraction/generation/evaluation.
- File and concurrency limits, queues/retries, and timeouts.
- Definitive SQL engine and migrations.
- Deployment, observability, and backups.
