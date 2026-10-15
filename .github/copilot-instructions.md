# Copilot instructions

## Project structure and architecture

- The app is a self-contained Korean-language space quiz in `index.html`. Its markup, inline SVG illustrations, CSS, quiz data, and browser-side JavaScript are kept together; there is no separate application framework or build pipeline.
- The `questions` array is the source of truth for quiz content. Each entry provides a category, question, four answer strings, a zero-based `correct` answer index, and an explanation. Each round shuffles a copy into `roundQuestions`, preserving answer order and the original data. The quiz records responses for a collapsible incorrect-answer review on the results screen.
- Results can be copied as Korean plain text. If clipboard access is unavailable or fails, show an explicit message and a selectable read-only text area. Guard asynchronous clipboard completion with `roundId` so a previous round cannot update a new round's UI.
- JavaScript renders and updates the existing page through element IDs and DOM APIs. Keep content inserted from quiz data as text (`textContent` or text nodes), and create answer controls as buttons rather than embedding data into HTML.
- Styling is in the document’s `<style>` block. It uses CSS custom properties for the color palette, includes light/dark color-scheme support, responsive layout rules, and reduced-motion handling.

## Build, test, and lint

- No build, test, or lint commands are configured; the repository has no package manifest or test suite.
- To run the app, open `index.html` in a browser. For a manual smoke check, answer all 10 questions, confirm progress and score update, check the results and incorrect-answer review, then use **다시 탐험하기** and confirm the quiz resets and shuffles without duplicate questions. Check **결과 복사** with clipboard access allowed and denied; the latter must provide manual copying. Also check a perfect score, keyboard focus, narrow layouts, and light/dark themes.

## Code conventions

- Keep user-facing quiz text in Korean and preserve the existing Korean wording/style when editing related UI.
- Keep quiz facts and explanations with their question data; `correct` is a zero-based index into that entry’s `answers`.
- The page relies on stable IDs as JavaScript selectors. When changing markup, update corresponding script references and retain the accessibility relationships and status/progress semantics (`aria-labelledby`, live feedback, and progress values).
- The quiz is intentionally dependency-free and self-contained. Keep changes within `index.html` unless a requirement calls for introducing additional assets or tooling.
