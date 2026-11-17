
# LumiLearn

## Overview

LumiLearn is an educational application designed to
help parents support their children's reading
comprehension and learning.

The application uses artificial intelligence to
extract text from textbook pages, generate quizzes,
evaluate student responses, and track learning progress.

## Main Features

- Parent registration and authentication.
- Student profile management.
- Progressive textbook image uploads.
- Full-text and highlighted-text extraction.
- Review and correction of extracted text.
- Consolidation of multiple textbook pages.
- AI-generated comprehension quizzes.
- Parent-approved questionnaires.
- AI-assisted assessment with parental approval.
- Repeated practice based on previous mistakes.
- Student progress and learning history.

## Technology Stack

The proposed technology stack includes:

### Frontend
- React
- TypeScript

### Backend
- Node.js
- Express
- TypeScript

### Database
- Relational database (see `docs/stack.md`)

### Artificial Intelligence
- OpenAI API

Final technology decisions are documented in
`docs/stack.md`.

## Project Structure

```text
LumiLearn/
├── AGENTS.md
├── README.md
├── docs/
│   ├── requirements.md
│   ├── architecture.md
│   ├── stack.md
│   └── implementation-plan.md
├── frontend/
└── backend/
```

## Documentation

- [Requirements](docs/requirements.md)
- [Architecture](docs/architecture.md)
- [Technology Stack](docs/stack.md)
- [Implementation Plan](docs/implementation-plan.md)
- [Codex Instructions](AGENTS.md)

## Development Approach

LumiLearn follows an incremental,
requirements-driven development process.

Each functional requirement is:

1. Analyzed.
2. Planned.
3. Approved.
4. Implemented.
5. Tested.
6. Reviewed.

Codex assists with implementation following
the instructions defined in `AGENTS.md`.

## Project Status

**Status:** Planning and initial development.

**Current priority:** RF-004 — Progressive Text Extraction.

The application is not yet ready for production.
