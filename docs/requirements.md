# LumiLearn — Product requirements

**Version:** 0.2 (draft)  
**Status:** Pending functional approval

## 1. Objective

Allow parents to prepare reading materials from images of school books and progressively assess their children's reading comprehension. A document may include multiple pages added at different times. For each page, the parent chooses to extract all visible text or only highlighted text, reviews the result, and confirms it. The system consolidates the content, generates quizzes, and proposes evaluations of the answers. The parent reviews, adjusts, and approves the evaluation, and may request new rounds as often as desired. History is kept per student.

## 2. Actors
- **Parent:** manages students, documents, questions, assignments, and final evaluations.
- **Student:** answers the quizzes assigned to them.
- **AI service (external component):** helps extract text, generate questions, and propose evaluations; it does not make final decisions about the student.

## 3. Functional requirements

### RF-001 — Parent registration and authentication
**Acceptance criteria**
- CA-001: Can create an account with an email address and password.
- CA-002: Duplicate registered email addresses are not allowed.
- CA-003: Can log in with valid credentials; invalid credentials are rejected.
- CA-004: Can log out.
- CA-005: Private resources require an authorized session.

### RF-002 — Student profiles
**Acceptance criteria**
- CA-001: The parent can create a profile with a name or alias and school level.
- CA-002: Can list and edit their profiles.
- CA-003: Each profile belongs to the account that created it.
- CA-004: A parent cannot view or edit profiles belonging to another account.

### RF-003 — Progressive image upload
**Description:** A study document may contain one or more pages. Images are added progressively, without requiring an initial bulk upload.

**Acceptance criteria**
- CA-001: The parent creates a study document with a title.
- CA-002: Can upload a JPG or PNG image and associate it with the document.
- CA-003: Can add other images to the same document at later times.
- CA-004: Adding a page does not delete or modify previous pages.
- CA-005: Can view images and their current order.
- CA-006: Can reorder pages.
- CA-007: Can delete a page after confirmation without deleting the others.
- CA-008: The system rejects invalid formats with an understandable message.
- CA-009: Pages and their order persist after logout or server restart.
- CA-010: Only the authorized owner can modify the document.

### RF-004 — Progressive extraction and text consolidation
**Description:** Each page is processed independently. The parent chooses **full text** or **highlighted text only using a fluorescent marker**. Consolidated text follows page order.

**Acceptance criteria**
- CA-001: Can select a page in the document.
- CA-002: Can choose full or highlighted mode before extracting.
- CA-003: In full mode, the system attempts to extract all readable text from the image.
- CA-004: In highlighted mode, the system attempts to extract only text identified as highlighted.
- CA-005: The result is shown together with its page and the mode used.
- CA-006: Extracted text and extraction mode are saved per page.
- CA-007: Extracting a new page does not reprocess or modify previous pages.
- CA-008: Can repeat extraction for a specific page without affecting other pages.
- CA-009: If no text is recognized or no highlight is detected, the system reports it and allows correction or a mode change.
- CA-010: Extraction failures are reported without losing previously saved data.
- CA-011: The system builds a consolidated view with pages in their current order.
- CA-012: When pages are added, reordered, or deleted, the consolidated view reflects the new set and order.
- CA-013: The result and its page association persist after server restart.
- CA-014: Extracted text is not considered confirmed automatically.

### RF-005 — Progressive correction and confirmation
**Acceptance criteria**
- CA-001: The parent can view and edit the text of each page.
- CA-002: Can save changes without confirming the page yet.
- CA-003: Can individually confirm a reviewed page.
- CA-004: Pages still pending review are identified.
- CA-005: Corrections to one page do not alter other pages.
- CA-006: The consolidated view uses corrected text from each page and respects its order.
- CA-007: Can continue adding pages after confirming others.
- CA-008: The complete document can be confirmed only if all current pages are confirmed and usable content exists.
- CA-009: Only confirmed consolidated text can be used to generate a quiz.
- CA-010: Corrections and confirmations persist after logout or server restart.
- CA-011: If a page is modified, added, reordered, or deleted after document confirmation, the document requires confirmation again before generating a new quiz.

### RF-006 — Quiz generation
**Acceptance criteria**
- CA-001: The parent requests questions based on a confirmed version of the consolidated text.
- CA-002: Can specify how many questions to generate.
- CA-003: The system returns questions relevant to the text and reference answers.
- CA-004: The quiz and questions are saved and associated with the content version used.
- CA-005: The system reports generation errors without deleting confirmed content.
- CA-006: Initially generated questions remain pending review.

### RF-007 — Question review and approval
**Acceptance criteria**
- CA-001: The parent can view questions and their reference answers.
- CA-002: Can edit or delete questions before approving them.
- CA-003: Can request question regeneration before approving the quiz.
- CA-004: Can approve the quiz.
- CA-005: Only approved quizzes can be assigned to students.

### RF-008 — Student assignment
**Acceptance criteria**
- CA-001: The parent selects one of their students and an approved quiz.
- CA-002: The assignment is saved and linked to the student.
- CA-003: The student can view assigned quizzes according to the approved access model.
- CA-004: Quizzes from another account cannot be assigned without authorization.

### RF-009 — Student response
**Acceptance criteria**
- CA-001: The student can open an assigned quiz.
- CA-002: Can record an answer for each question.
- CA-003: Can submit the attempt for evaluation.
- CA-004: The system preserves answers, date, student, and quiz.
- CA-005: Submitted answers remain available for review.

### RF-010 — Mixed evaluation with parent approval
**Acceptance criteria**
- CA-001: The system compares answers with references and proposes a grade per question.
- CA-002: Presents a provisional overall score and reviewable explanations.
- CA-003: The parent can view the original answers and references.
- CA-004: Can modify grades and add notes.
- CA-005: Can explicitly approve the final evaluation.
- CA-006: The system distinguishes provisional from approved evaluations.
- CA-007: Preserves the original proposal and the final approved version.
- CA-008: An automated proposal is never presented as a clinical diagnosis or definitive evaluation without the parent's approval.

### RF-011 — Repetition and reinforcement
**Acceptance criteria**
- CA-001: The parent can request another quiz based on the same confirmed content.
- CA-002: Can repeat the process as often as desired, subject to explicit technical or service limits.
- CA-003: The system can generate new questions focused on concepts missed in previous attempts.
- CA-004: Previous quizzes and attempts are not overwritten.
- CA-005: Each new quiz can be assigned to the same student.
- CA-006: The system may retain a question bank by document or topic for future reuse; exact selection rules remain pending.

### RF-012 — History and progress tracking
**Acceptance criteria**
- CA-001: The parent can view quizzes completed by each student.
- CA-002: Can view answers, dates, proposed evaluations, and approved evaluations.
- CA-003: Can compare results between attempts for the same content.
- CA-004: History persists after logout or server restart.
- CA-005: A quiz retains a reference to the text version used to generate it, even if the document is edited later.
- CA-006: A parent cannot view the history of students belonging to another account.

## 4. Non-functional requirements
- **NFR-001 Security:** passwords use robust hashing; sessions are protected.
- **NFR-002 Authorization:** owner-based controls for documents, students, questions, and history.
- **NFR-003 Secrets:** AI keys only in the backend and environment variables; never in the repository or browser.
- **NFR-004 Persistence:** preserve documents, pages, text, versions, quizzes, and attempts across restarts.
- **NFR-005 Validation:** validate file type/size and input data; specific limits are pending.
- **NFR-006 Resilience:** clear errors and safe retries without loss of corrections.
- **NFR-007 Child privacy:** minimal collection, restricted access, and retention policy to be defined.
- **NFR-008 Maintainability:** modularity, separation of responsibilities, and tests.
- **NFR-009 Testing:** unit/integration tests and E2E tests for critical flows.
- **NFR-010 Traceability:** preserve source text/versions and evaluation approval states.

## 5. Cross-cutting business rules
- A document contains ordered pages; each page retains its image, extraction mode, extracted text, corrected text, and review status.
- The consolidated view is derived from corrected text of current pages in their order, avoiding duplicate sources of truth.
- The document can be confirmed only when all current pages have been reviewed and usable content exists.
- Any subsequent change to pages invalidates confirmation **for new generations**, but does not alter previous versions used in existing quizzes.
- Each quiz stores a reference or immutable snapshot of the confirmed content version used.
- Automated evaluations are provisional; only the parent approves the final evaluation.
- Previous attempts and their evaluations are not overwritten when practice is repeated.

## 6. Main dependencies
RF-001 → RF-002 and RF-003 → RF-004 → RF-005 → RF-006 → RF-007 → RF-008 → RF-009 → RF-010 → RF-011 / RF-012. RF-008 also requires RF-002. RF-011 may use results from RF-010; RF-012 adds history for the preceding requirements.

## 7. Pending approval decisions
1. Initial question types (multiple choice, open-ended, or both).
2. Student access (parent session, own account, or both).
3. Grading scale (percentage, descriptive levels, or both) and thresholds, if used.
4. Question bank: rules for reusing, mixing, and prioritizing errors.
5. Initial languages (FR/ES/EN proposed, not approved).
6. Image-size limits, pages per document, and AI quota.
7. Handling pages without highlights, multiple colors, handwriting, and illegible content.
8. Retention and deletion policy for children's information.
9. Behavior of pending quizzes when the document is edited.
10. Whether documents without a student account are allowed or must be associated with one.

**Note:** Examples of 5 or 10 pages do not constitute a maximum page limit.
