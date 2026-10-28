# Group B Project: Flashcard Quiz

## 📝 Analysis

**Problem**

Students preparing for tests need to recall facts without looking at their notes. Re-reading material can make it feel familiar without showing whether they can remember it independently. This makes it difficult to identify gaps in their knowledge and decide which topics need more practice. When studying several chapters, students can also lose track of recurring mistakes and whether their recall is improving over time.

**Scenario**

Before a test, a student wants to check what they can remember from a chapter without consulting their notes. They select the chapter and answer its questions. Afterwards, they review their mistakes, retry difficult questions and compare the result with previous attempts. They can also add or correct flashcards as their study material changes.

**Proposed solution**

We propose a small Python terminal application that lets learners practise flashcards by chapter, receive feedback, review mistakes and compare quiz attempts. Flashcards and quiz results are stored in local files.

Each flashcard contains a chapter, a question and one predefined short answer, such as a word or a brief factual phrase. The app compares the submitted answer with the predefined answer after ignoring capitalization and removing leading and trailing spaces from both. Otherwise, the answers must match exactly; the app does not assess unrestricted written responses or accept alternative wording automatically. Empty answers, including answers containing only spaces, are rejected without advancing the quiz.

A normal quiz asks all available questions from the selected chapter once, in a random order. There is no fixed five-question limit or option to choose the number of questions. A retry asks only the questions answered incorrectly in the preceding attempt.

App flow:

1. Show a menu to start a quiz, view past scores, manage flashcards or quit.
2. Let the player choose a chapter and load all questions from that chapter in a random order.
3. Show questions one at a time, display progress, check answers and give feedback.
4. Show the final result and save it as a separate attempt.
5. Allow the player to review or retry mistakes, view past scores or return to the menu.

### 👤 User Roles

| Role | Description |
|------|-------------|
| Learner | A student who practises chapter material, adds and edits their own flashcards, reviews mistakes and compares quiz results over time. |

The same learner manages the flashcards and takes quizzes. The project does not require separate accounts or administrator roles.

### 📖 User Stories

Each student is responsible for three project-specific stories. Every story has a unique ID and a named owner. Acceptance criteria use **Given** for the starting context, **When** for the action or event, and **Then** for the observable result.

#### US-01: Add flashcards

**Responsible:** Marisa

As a learner, I want to add new flashcards so that I can expand my study material.

**Acceptance criteria**

- **Given** I have chosen to add a flashcard, **when** I enter a non-empty chapter, question and correct answer and confirm saving, **then** the flashcard is saved to the file.
- **Given** a required field is empty or contains only spaces, **when** I try to save the flashcard, **then** the app displays an error, saves no new flashcard and lets me correct the input.
- **Given** a new flashcard has been saved successfully, **when** I restart the app and select its chapter, **then** the new flashcard is available for a quiz.

#### US-02: Final score

**Responsible:** Marisa

As a learner, I want to see my final score so that I know how well I performed.

**Acceptance criteria**

- **Given** I am answering the last question of an attempt, **when** I submit a non-empty answer, **then** the app displays the final numbers of correct and incorrect answers.
- **Given** all questions in an attempt have been answered, **when** the final result is displayed, **then** the percentage equals the number of correct answers divided by the total number of questions, multiplied by 100.
- **Given** a chapter contains five questions and I answer three correctly, **when** the final result appears, **then** it shows three correct answers, two incorrect answers and 60%.
- **Given** I answer every question incorrectly, **when** the final result appears, **then** it shows zero correct answers and 0%.

#### US-03: Review mistakes

**Responsible:** Marisa

As a learner, I want to review my incorrect answers so that I know what to study again.

**Acceptance criteria**

- **Given** I have completed an attempt with incorrect answers, **when** I choose to review mistakes, **then** the app shows each incorrectly answered question, my submitted answer and the correct answer from that attempt.
- **Given** I have completed an attempt without incorrect answers, **when** I choose to review mistakes, **then** the app displays "No mistakes to review."

---

#### US-04: Choose a chapter

**Responsible:** Dayhe Kim

As a learner, I want to choose a chapter so that I can focus on the material I need to study.

**Acceptance criteria**

- **Given** chapters are available, **when** I start a quiz, **then** the app displays them in a numbered menu.
- **Given** the chapter menu is displayed, **when** I select a valid chapter, **then** the quiz starts using only questions from that chapter.
- **Given** the chapter menu is displayed, **when** I enter a selection that is not listed, **then** the app displays an error and lets me try again without starting a quiz.
- **Given** no chapters are available, **when** I try to start a quiz, **then** the app displays an explanatory message.

#### US-05: View quiz progress

**Responsible:** Dayhe Kim

As a learner, I want to see my progress during a quiz so that I know how many questions are left.

**Acceptance criteria**

- **Given** an attempt contains N questions, **when** a question is displayed, **then** the app shows its position as "Question X of N", starting with "Question 1 of N".
- **Given** the current question is not the last one, **when** I submit a non-empty answer, **then** the next question appears and the question number increases by one.
- **Given** the last question is displayed, **when** I submit a non-empty answer, **then** the attempt ends and displays my final result.

#### US-06: View past scores

**Responsible:** Dayhe Kim

As a learner, I want to view my past scores so that I can compare my performance over time.

**Acceptance criteria**

- **Given** previous results exist, **when** I select "Past Scores", **then** the app displays them newest first.
- **Given** previous results exist, **when** I select "Past Scores", **then** each displayed result includes the chapter, date/time, correct answers out of total questions and percentage.
- **Given** no results exist, **when** I select "Past Scores", **then** the app displays "No previous results."

---

#### US-07: Check answers

**Responsible:** Rui

As a learner, I want feedback after each answer so that I can learn from mistakes.

**Acceptance criteria**

- **Given** a quiz question is displayed, **when** I submit a non-empty short answer, **then** the app compares it with the predefined answer and displays whether it is correct or incorrect.
- **Given** the predefined answer is "Paris", **when** I submit "  pArIs  ", **then** the app accepts it as correct.
- **Given** the predefined answer is "Paris", **when** I submit "Lyon", **then** the app marks the answer incorrect and displays "Paris" as the correct answer.
- **Given** a quiz question is displayed, **when** I submit an empty answer or only spaces, **then** the app displays an error without changing the score or advancing the quiz.

#### US-08: Edit flashcards

**Responsible:** Rui

As a learner, I want to edit existing flashcards so that I can correct mistakes in my study material.

**Acceptance criteria**

- **Given** flashcards exist, **when** I choose to edit a flashcard, **then** the app lets me select one from a chapter.
- **Given** I have selected a flashcard to edit, **when** I enter a non-empty question and correct answer and confirm saving, **then** the app saves the changes to the file.
- **Given** an edited required field is empty or contains only spaces, **when** I try to save the changes, **then** the app displays an error, preserves the saved flashcard and lets me correct the input.
- **Given** changes to a flashcard have been saved successfully, **when** I restart the app and select that flashcard, **then** its updated question and correct answer are available.

#### US-09: Filter past scores

**Responsible:** Rui

As a learner, I want to filter past scores by chapter so that I can track my progress in a particular subject.

**Acceptance criteria**

- **Given** previous results exist, **when** I choose to filter scores, **then** I can select a chapter or show all results.
- **Given** the score-filter menu is displayed, **when** I select a chapter, **then** only results for that chapter are displayed, newest first.
- **Given** the score-filter menu is displayed, **when** I enter a selection that is not listed, **then** the app displays an error and lets me try again.
- **Given** no saved results exist for a chapter, **when** I filter scores by that chapter, **then** the app displays an explanatory message.

---

#### US-10: Load flashcards

**Responsible:** Amanuel

As a learner, I want flashcards loaded from a file so that study material can be updated without changing the code.

**Acceptance criteria**

- **Given** a valid flashcard file exists, **when** the app starts, **then** it loads each flashcard's chapter, question and correct answer.
- **Given** new flashcards have been added to the file, **when** the app restarts, **then** those flashcards are available.
- **Given** the file is missing, unreadable or incorrectly formatted, **when** the app tries to load it, **then** it displays an error without crashing or overwriting the file.
- **Given** the file is empty, **when** I try to start a quiz, **then** the app explains that no questions are available.

#### US-11: Random questions

**Responsible:** Amanuel

As a learner, I want questions to appear in a random order so that I can practise without memorizing their sequence.

**Acceptance criteria**

- **Given** a chapter contains N flashcards, **when** I select it and start a normal quiz, **then** the quiz includes all N flashcards.
- **Given** the question set for an attempt is ready, **when** the attempt starts, **then** the app shuffles the set before presenting the first question. A shuffled order may happen to match a previous order.
- **Given** an attempt contains N flashcards, **when** I complete the attempt, **then** each of those N flashcards has been asked exactly once.
- **Given** a chapter contains one flashcard, **when** I start a normal quiz for that chapter, **then** that flashcard is asked exactly once and the attempt ends after I submit a non-empty answer.

#### US-12: Retry mistakes

**Responsible:** Amanuel

As a learner, I want to retry questions I answered incorrectly so that I can practise difficult material.

**Acceptance criteria**

- **Given** the most recently completed attempt contains incorrect answers, **when** I choose "Retry Mistakes", **then** a new attempt starts with exactly those incorrectly answered questions, each asked once in a random order.
- **Given** the most recently completed attempt contains incorrect answers, **when** I start a retry, **then** its correct-answer count starts at zero and its total question count equals the number of questions being retried.
- **Given** a retry is in progress and the results file is writable, **when** I submit a non-empty answer to its last question, **then** its result is saved as a separate attempt without changing previous results.
- **Given** the most recently completed attempt has no incorrect answers, **when** I choose "Retry Mistakes", **then** the app explains that there are no questions to retry and does not start a new attempt.

### Shared functionality

Some basic features are needed for the application to work. These are shared responsibilities of the group rather than individual user stories.

- Provide a main menu with options to start a quiz, view past scores, manage flashcards and quit.
- Automatically save each completed quiz or retry as a separate attempt with the chapter, date/time, total questions, correct answers and percentage.
- Keep previous results when new results are saved and make them available after restarting the application.
- Display an error if saving fails, while still showing the learner their final result.
- Handle invalid menu inputs and file errors without crashing.

### Use cases

- Add or edit a flashcard in a chapter.
- Select a chapter and answer all its flashcards in a random order.
- Check answers and view quiz progress.
- View the final score, review mistakes and retry incorrectly answered questions.
- View past scores and filter them by chapter.
- Exit the application while keeping saved flashcards and results.

---

## ✅ Project Requirements

The quiz is currently at the proposal stage. The following describes how the planned application will meet the three requirements in the course reference template.

### 1. Interactive App (Console Input)

The learner will interact with the application through the terminal. They will be able to:

- Choose a chapter from a numbered menu.
- Enter short answers and receive feedback.
- See the current question number and final score.
- Add and edit flashcards.
- Review and retry mistakes.
- View previous results and filter them by chapter.

### 2. Data Validation

The application will validate input before using or saving it:

- **Menu selections:** Reject options that are not listed, display an error and let the learner try again.
- **Flashcard fields:** Require a chapter, question and correct answer. Empty fields and fields containing only spaces will be rejected.
- **Quiz answers:** Reject empty answers and answers containing only spaces without changing the score or advancing the quiz.
- **Answer comparison:** Ignore capitalization and surrounding spaces; otherwise require an exact match with the predefined answer. For example, `  pArIs  ` will match `Paris`, while `Lyon` will be incorrect.
- **Flashcard files:** Display an error for missing, unreadable or incorrectly formatted files without crashing or overwriting them. An empty file will prevent a quiz from starting and produce an explanatory message.
- **Saving results:** Display an error if saving fails while still showing the learner their final result.

### 3. File Processing

The application will read flashcards from a local file, save added or edited flashcards, and store completed quiz attempts. Saved data will remain available after restarting.

CSV is the proposed storage format. The filenames and examples below describe the planned data files; these files have not been implemented yet.

**Flashcard file: `flashcards.csv`**

Each row will contain a chapter, question and predefined answer.

```csv
chapter,question,answer
Geography,What is the capital of France?,Paris
Geography,What is the capital of Portugal?,Lisbon
```

**Results file: `results.csv`**

Each completed quiz or retry will append a separate row with the chapter, completion date/time, total questions, correct answers and percentage. Existing results will be preserved.

```csv
chapter,completed_at,total_questions,correct_answers,percentage
Geography,2026-10-28T14:30:00,2,1,50
Geography,2026-10-28T14:35:00,1,1,100
```

These example rows show a two-question quiz followed by a retry of its one incorrect answer. The CSV reader and writer will handle quoting for fields containing commas.

---

## ⚙️ Implementation

The repository currently contains the project proposal and a `hello_world.py` starter script. The flashcard quiz features described above are planned and have not been implemented yet.

### Technology

- Language: Python 3.x.
- Planned interface: console application.
- Development environment: Visual Studio Code or GitHub Codespaces.
- Planned storage: local CSV files.
- No external packages are currently used or planned.

### 📂 Repository Structure

Current structure:

```text
group-b-project/
├── hello_world.py    # starter script that prints a greeting
├── LICENSE           # MIT license
└── README.md         # project analysis, stories and implementation plan
```

Planned additions:

```text
main.py              # quiz application entry point
flashcards.csv       # study material and saved flashcard changes
results.csv          # completed attempts, created when results are saved
```

The team will update this section as the application is implemented.

### How to Run

To run the existing starter script:

1. Open the project folder in Visual Studio Code or GitHub Codespaces.
2. Open a terminal in the project folder.
3. Run:

   ```bash
   python3 hello_world.py
   ```

Expected output:

```text
hello world
```

The full quiz is not runnable yet. Its run instructions will be added when the entry point is implemented.

### Libraries Used

The current starter script imports no libraries. The quiz is expected to use these Python standard library modules:

| Module | Planned purpose |
|--------|-----------------|
| `csv` | Read and write flashcards and quiz results. |
| `random` | Shuffle questions for each attempt. |
| `datetime` | Record when an attempt was completed. |
| `pathlib` | Work with local data-file paths. |

The team will update this list to match the actual imports before final submission.

---

## 👥 Team & Contributions

The following table records planned responsibilities. It will be updated with actual contributions as implementation progresses.

| Name | Assigned stories | Planned contribution |
|------|------------------|----------------------|
| Marisa | US-01, US-02, US-03 | Add flashcards, calculate and display final scores, and review mistakes. |
| Dayhe Kim | US-04, US-05, US-06 | Chapter selection, quiz progress and past-score display. |
| Rui | US-07, US-08, US-09 | Answer checking and feedback, flashcard editing and score filtering. |
| Amanuel | US-10, US-11, US-12 | Flashcard loading, random question order and retrying mistakes. |
| Whole group | Shared functionality | Main menu, saving results, shared error handling and integration. |

## 🤝 Contributing

- Use this repository as a starting point by importing it into your own GitHub account.
- Work only within your own copy — do not push to the original template.
- Commit regularly to track your progress.

The documentation structure follows the [PizzaRP Pizzeria Reference Project](https://github.com/Python-Foundations-Programming/PizzaRP-Pizzeria-Reference-Project), adapted to this group's flashcard quiz.

## 📝 License

This project is developed for educational use as part of the Programming Foundations module and is licensed under the [MIT License](LICENSE).
