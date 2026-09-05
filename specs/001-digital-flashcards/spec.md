# Feature Specification: Digital Flashcards Learning Webapp

**Feature Branch**: `001-digital-flashcards`

**Created**: 2026-09-05

**Status**: Draft

**Input**: User description: "Build a webapp that helps someone learning through the use of digital flashcards. The interface will let the user create flashcards, answer flashcard quizzes and view his own statistics. The flashcards will each have a subject category, a school level and a type (which defines how the flashcard works). Each user will have a separate profile."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Create and Organize Flashcards (Priority: P1)

As a learner, I want to create flashcards so that I can build a study collection suited to my needs. Each flashcard has a question on its face and an answer on its back. Each card must be classified with:
- one subject category (examples: Mathematics, French, etc.)
- one school level (examples: CP, CE1, CE2, CM1, etc.)
- one flashcard type (examples: basic question-and-answer, multiple-choice, and dictation); and
- the authenticated account that created the card, recorded as creator metadata.

These classifications are part of the card's definition. They must be selected or entered while creating the card, and be available for filtering and statistics. All cards belong to one shared application collection and are available to every learner profile. The creator metadata is informational only and is not a card ownership boundary or filter.

**Why this priority**: User-created learning content is the foundation of the product and must be available before quizzes or statistics provide meaningful value.

**Independent Test**: An authenticated account can create, edit, view, and delete a flashcard, assign its required fields, and a different account or learner profile can confirm that the card appears in the shared application collection.

**Acceptance Scenarios**:

1. **Given** an authenticated account is creating a flashcard, **When** the account selects a subject category, school level, and type, enters the required question and answer content, and saves it, **Then** the flashcard is added to the shared application collection with all classifications and the creating account recorded as metadata.
2. **Given** a flashcard type has type-specific fields, **When** the user selects that type, **Then** the creation form displays only the fields needed for that type and explains how the card will work in a quiz.
3. **Given** a user selects the basic flashcard type, **When** the user enters a question and its plain-text answer, **Then** the card is configured to show a text input for the learner to type an answer during a quiz.
4. **Given** a user selects the multiple-choice flashcard type, **When** the user enters a question and four answer options with exactly one correct answer and three incorrect answers, **Then** the card is configured to present those four options for the learner to choose from during a quiz.
5. **Given** a user selects the dictation flashcard type, **When** the user enters the dictated phrase that the learner must write down, **Then** the card is configured to keep the phrase hidden during practice and play it through speech synthesis when the learner requests it.
6. **Given** a user submits an incomplete or invalid flashcard, **When** the user tries to save it, **Then** the system identifies each missing or invalid classification or content field and does not create the card.
7. **Given** a user opens a flashcard, **When** the user edits or deletes it, **Then** the application reflects the change and the user is asked to confirm deletion before the card is removed.
8. **Given** an authorized user opens a saved flashcard, **When** the user views its details, **Then** the subject category, school level, type, and creator metadata are displayed with the card content, without offering creator-based filtering.

---

### User Story 2 - Practice With Flashcard Quizzes (Priority: P1)

As a learner, I want to answer quizzes generated from my flashcards so that I can practice recalling what I have learned and receive immediate feedback.

**Why this priority**: Practice is the core learning loop and turns stored flashcards into an active learning experience.

**Independent Test**: An authenticated account can select a learner profile, start a quiz from that profile's collection or classification, answer cards one at a time, see whether each answer is correct, and finish with a summary of the attempt.

**Acceptance Scenarios**:

1. **Given** a user has flashcards for his own school level or below, **When** the user starts a quiz and chooses available filters such as subject category, school level, and flashcard type, along with the number of cards to answer, **Then** the system presents matching cards one at a time and shows quiz progress.
2. **Given** the selected filters match at least one card but fewer cards than the requested number of questions, **When** the user tries to start the quiz, **Then** the quiz does not start and the system shows an error explaining that the requested number of questions exceeds the available cards.
3. **Given** a user has flashcards **When** the user starts a quiz **Then** the system presents cards by selecting them at random but more frequently when the score is low for user/card couple.
4. **Given** a quiz presents a card, **When** the user submits an answer, **Then** the system evaluates it according to the card type, shows the correct answer and feedback, and allows the user to continue.
5. **Given** a quiz presents a basic flashcard, **When** the learner types an answer and submits it, **Then** the system compares the submitted text with the card's plain-text answer, ignores differences in leading or trailing whitespace and letter case, and displays whether it is correct.
6. **Given** a quiz presents a non-dictation card, **When** the card is displayed, **Then** the system automatically reads the card's visible question aloud and does not display a speaker icon on the card.
7. **Given** a quiz presents a dictation card, **When** the learner views the card, **Then** the dictated phrase is not displayed, a speaker icon is visible on the card, and activating the icon reads the phrase aloud.
8. **Given** a dictation card has been presented, **When** the learner types and submits a written answer, **Then** the system evaluates it against the card's expected written answer, displays correctness feedback, and reveals the expected answer after submission.
9. **Given** any quiz card has been displayed, **When** the learner clicks the card, **Then** the system replays that card's spoken content, whether or not the card displays a speaker icon.
10. **Given** a user has submitted an answer to a quiz card, **When** correctness feedback is displayed, **Then** the system reads the correct answer and feedback aloud while keeping the feedback visible as text.
11. **Given** a quiz presents a card, **When** the user submits an answer, **Then** the system stores the date of the day as the last played date, for the card and player couple.
12. **Given** a quiz presents a card, **When** the user submits a correct answer, **Then** the system adds a point to the card/user couple.
13. **Given** a quiz presents a card, **When** the user submits an incorrect answer, **Then** the system subtracts a point from the card/user couple.
14. **Given** a user completes a quiz, **When** the final answer is submitted, **Then** the system shows the number and percentage of correct answers and records the attempt for that user's statistics.
15. **Given** a user has no cards matching the selected quiz filters, **When** the user tries to start the quiz, **Then** the system explains that no cards are available and offers a way to change the filters or create a card.

---

### User Story 3 - Review Personal Statistics (Priority: P2)

As a learner, I want to view my own study statistics so that I can understand my progress and decide what to practice next. Each learner profile has separate statistics, even when profiles are managed by the same authenticated account.

**Why this priority**: Statistics help learners reflect on progress and identify weak areas after the creation and quiz loop is working.

**Independent Test**: An authenticated account can select a learner profile with quiz history, practice cards from the shared application collection, open the statistics view, and verify that the displayed totals and breakdowns match only that profile's recorded quiz attempts.

**Acceptance Scenarios**:

1. **Given** a selected learner profile has completed quiz attempts, **When** the account opens statistics, **Then** the system shows that profile's total attempts, cards answered, correct-answer rate, and recent activity.
2. **Given** a selected learner profile has quiz history across classifications, **When** the account views statistics, **Then** the system provides breakdowns by subject category, school level, and flashcard type using the classifications recorded on that profile's cards.
3. **Given** a selected learner profile has no quiz history, **When** the account opens statistics, **Then** the system shows an informative empty state and a clear path to start studying for that profile.
4. **Given** an authenticated account has multiple learner profiles with activity, **When** the account switches between profiles and opens statistics, **Then** each profile shows only its own quiz results and learning data.

---

### User Story 4 - Manage Household Learner Profiles (Priority: P1)

As an authenticated account holder, such as a parent, I want to create and select separate learner profiles for people in my household so that each person has an individual card collection and learning history.

**Why this priority**: Profile separation is necessary for trustworthy statistics and allows one authorized account to support several household learners.

**Independent Test**: One authenticated account can create at least two named learner profiles, practice cards from the shared application collection under each profile, switch between them, and verify that each profile has separate statistics while both can use the same cards.

**Acceptance Scenarios**:

1. **Given** a visitor does not have an active authenticated account, **When** the visitor attempts to access the app, **Then** the system requests authentication before allowing access.
2. **Given** an authenticated account is authorized to use the app, **When** the account creates a learner profile with a name, **Then** the profile becomes available for selection and has independent quiz history and statistics while using the shared application card collection.
3. **Given** an authenticated account has multiple learner profiles, **When** the account selects a profile, **Then** quizzes and statistics use only the selected profile's data while cards remain available from the shared application collection.
4. **Given** an authenticated account creates multiple learner profiles, **When** the account updates a profile name or removes a profile, **Then** the change applies only to that profile and the system handles its associated cards and history without exposing them through another profile.

### Edge Cases

- A user tries to save a flashcard with whitespace-only content, a missing classification, or a type-specific field in an invalid format.
- A subject category, school level, or flashcard type is removed or renamed after cards already use it; existing cards retain a valid display value and remain usable.
- A quiz is interrupted by a lost connection or the user leaving the page; completed answers are not counted twice and the user receives a clear recovery or restart path.
- Spoken audio is unavailable, fails to start, or is disabled; the card remains fully usable through visible text where applicable and typed or selectable answers, and clicking the card does not block quiz progress.
- A dictation card's phrase is accidentally exposed before submission; the phrase remains hidden during practice and is only revealed as the expected answer after submission.
- A user deletes a flashcard that appears in prior quiz history; historical statistics remain understandable without exposing the deleted card's private content.
- An account attempts to access or modify another account's profiles, quiz attempts, or statistics, or attempts to apply creator-based access restrictions to a shared card.
- An authenticated account has no learner profiles, attempts to create duplicate profile names, or switches profiles while a quiz is in progress; the system preserves profile boundaries and provides a clear next action.
- A quiz contains a single card, repeated cards, or a large collection; progress and completion behavior remain correct in each case.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The system MUST require an authenticated account to be authorized before allowing access to the application.
- **FR-002**: The system MUST allow each authorized authenticated account to create and manage as many named learner profiles as needed for its household.
- **FR-003**: The system MUST associate each flashcard with the authenticated account that created it as creator metadata only, and MUST associate each quiz attempt and statistic with exactly one learner profile and its managing authenticated account.
- **FR-003a**: The system MUST require a selected learner profile for starting quizzes, recording quiz attempts, and viewing statistics, but MUST NOT require a profile to own or access a card.
- **FR-003b**: The system MUST keep quiz attempts and statistics separate between learner profiles managed by the same account while exposing the same shared card collection to all authorized users.
- **FR-003c**: The system MUST allow the account holder to create, rename, select, and remove learner profiles, with profile names required for identification.
- **FR-004**: Each flashcard MUST have exactly one subject category, exactly one school level, and exactly one type.
- **FR-005**: The system MUST validate required flashcard content and type-specific fields before saving a card.
- **FR-006**: The system MUST provide a type-specific authoring and quiz experience, with each supported type defining its required content, answer method, and evaluation behavior.
- **FR-007**: The initial release MUST support a basic question-and-answer flashcard type, a multiple-choice flashcard type, and a dictation flashcard type.
- **FR-007a**: For the basic flashcard type, the system MUST store one plain-text answer, present the learner with a text input during a quiz, and evaluate the submitted answer without requiring a choice from predefined options.
- **FR-007b**: When evaluating a basic flashcard answer, the system MUST ignore differences in leading or trailing whitespace and letter case, then provide immediate correctness feedback and reveal the stored answer.
- **FR-007c**: For the dictation flashcard type, the system MUST store one dictated phrase that serves as the expected written answer, keep the phrase hidden during practice, provide a speaker button that plays the phrase aloud, and accept a typed answer from the learner.
- **FR-007d**: When evaluating a dictation answer, the system MUST provide immediate correctness feedback and reveal the expected written answer only after the learner submits their response.
- **FR-008**: The system MUST allow an account to start a quiz for the selected learner profile using cards from the shared application collection and apply subject category, school level, and type filters, but not a creator filter.
- **FR-009**: The system MUST present quiz cards one at a time, show progress, accept an answer, and provide immediate correctness feedback before continuing.
- **FR-010**: The system MUST calculate and display quiz results, including total questions, correct answers, and percentage correct, when a quiz ends.
- **FR-011**: The system MUST record completed quiz attempts for the selected learner profile and the answer results needed to calculate that profile's statistics.
- **FR-012**: The system MUST display statistics for the selected learner profile, including total quiz attempts, cards answered, correct-answer rate, recent activity, and breakdowns by subject category, school level, and flashcard type.
- **FR-013**: The system MUST provide useful empty, loading, validation-error, and failure states for flashcard management, quizzes, statistics, and profile views.
- **FR-014**: The system MUST prevent an authenticated account from viewing, changing, or deleting another account's profiles, quiz attempts, or statistics; card visibility MUST NOT be restricted by creator account or learner profile.
- **FR-015**: The system MUST preserve aggregate quiz history when a shared flashcard is deleted, while avoiding display of deleted card content in historical results.
- **FR-016**: The interface MUST be usable with keyboard navigation, readable contrast, clear feedback, and responsive layouts on supported desktop and mobile screen sizes.
- **FR-017**: During a quiz, the system MUST automatically read each card's spoken prompt aloud when the card is displayed and read the correct answer and feedback aloud after submission; non-dictation prompts remain visible, while dictation phrases remain hidden until after submission.
- **FR-018**: The system MUST display a speaker icon only on dictation cards, and activating that icon MUST replay the dictated phrase.
- **FR-019**: Clicking any quiz card MUST replay its spoken content, including cards that do not display a speaker icon.

### Key Entities *(include if feature involves data)*

- **Authenticated Account**: An authorized account holder, such as a parent, who can manage household learner profiles and their associated learning data.
- **Learner Profile**: A named person within an authenticated account; owns that profile's quiz attempts and statistics but does not own cards.
- **Flashcard**: A shared application learning item containing prompt content, answer content, subject category, school level, interaction type, and creator account metadata without an ownership relationship.
- **Flashcard Type**: A supported interaction definition that determines authoring fields, answer input, and answer evaluation; the initial types are basic question-and-answer, multiple-choice, and dictation.
- **Subject Category**: A managed classification used to organize, filter, and report on flashcards by academic subject.
- **School Level**: A managed classification representing the intended educational level of a flashcard and determining which cards are eligible for a learner's quiz.
- **Quiz Attempt**: A completed or in-progress practice session for one learner profile, containing selected cards, submitted answers, results, and completion time, including the classifications used for selection and reporting.
- **Statistic**: A derived view of one learner profile's quiz history, including totals, rates, recency, and classification breakdowns.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: At least 90% of first-time users in usability evaluation can create a valid flashcard, including all required classifications, within 2 minutes without assistance.
- **SC-002**: At least 90% of users with available cards can start a filtered quiz and submit their first answer within 60 seconds.
- **SC-003**: At least 95% of completed quiz attempts display a result summary containing total questions, correct answers, and percentage correct immediately after completion.
- **SC-004**: For a shared application collection of 1,000 flashcards and a test learner profile with 100 quiz attempts, the statistics view displays the correct totals and classification breakdowns within 2 seconds for at least 95% of visits.
- **SC-005**: In multi-account and multi-profile privacy testing, 100% of tested attempts to access another account's profiles, quiz history, or statistics are denied or isolated, while authorized users can access shared cards without creator-based filtering.
- **SC-006**: At least 90% of usability-evaluation participants can identify their next study action from the empty states for a new account with no profiles, an empty quiz filter, and a learner profile with no quiz history.
- **SC-007**: The core study workflow remains usable without horizontal scrolling and without loss of essential actions at viewport widths from 320 pixels through 1440 pixels.
- **SC-008**: In usability testing with spoken audio enabled, at least 95% of presented quiz cards have their question and post-answer feedback read aloud or provide a clear audio-unavailable message within 3 seconds.

## Assumptions

- Authorized account holders may be parents or guardians managing profiles for people in their household; learners may use the product on desktop or mobile web browsers.
- The initial release uses an authenticated account with authorization to use the app; the exact authentication provider and authorization mechanism are implementation decisions.
- All flashcards are part of one shared application collection and are available to all authorized users in the initial release; creator metadata is informational and creator-based filtering is out of scope.
- The initial supported flashcard types are basic question-and-answer, multiple-choice, and dictation; additional types can be added through the same type-specific contract.
- Statistics are based on completed quiz attempts; abandoned or interrupted attempts are not included in completed-attempt totals unless explicitly resumed and completed.
- The product uses user-friendly error messages and preserves already-submitted quiz answers when recovery is possible.
- No import, export, spaced-repetition scheduling, social features, or instructor administration is included in this feature unless a later specification adds it.
