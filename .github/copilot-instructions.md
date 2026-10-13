# Copilot instructions

## Project shape

This is a dependency-free, single-page browser quiz. The entire implementation lives in
`index.html`:

- The `<style>` block contains all layout, theme, responsive, accessibility, and animation
  rules.
- The markup contains the quiz shell, mission-control status bar, progress bar, question
  area, feedback area, and hidden results screen.
- The `<script>` block owns the question data and all application state. `current` tracks
  the question index and `score` tracks correct answers. `renderQuestion()` rebuilds the
  answer buttons for the current item; `handleAnswer()` locks the options, updates
  feedback and score, and advances after a short delay; `showResults()` and
  `restartQuiz()` manage the end and reset states.

Keep the quiz functional without a server, bundler, package manager, external fonts, or
runtime dependencies. It is intended to open directly as a `file://` URL.

## Commands and validation

There is no `package.json`, build script, test runner, or lint configuration. There are no
automated build, test, or lint commands to run.

For manual validation, open `index.html` directly in a browser or use the integrated
browser preview. Check the initial question, keyboard focus and activation of native
answer buttons, correct and incorrect feedback, score/progress updates, the final results
screen, and the “Try Again” reset. Test both light and dark system color schemes and
reduced-motion preferences when changing visual behavior.

## Key conventions

- Keep changes self-contained in `index.html` unless a new requirement clearly justifies
  another file.
- Store quiz content in the `questions` array with zero-based `answer` indexes matching
  each `choices` array.
- Use native `<button type="button">` controls for interactive answers and actions so
  keyboard navigation remains available without custom event handling.
- Preserve the state flow and timing: answer buttons are disabled immediately after a
  selection, feedback is shown, and the next question advances after the existing
  850ms delay.
- Use the existing CSS custom properties for colors and surfaces, and add dark-theme
  overrides inside `@media (prefers-color-scheme: dark)` rather than hard-coding a
  separate theme.
- Preserve the existing visual language: centered narrow card, mission-control status
  bar, colorful progress gradient, green correct feedback, red shake feedback, and
  emoji-based result reactions.
- Keep status and transient feedback accessible: retain meaningful text in the status
  elements and use the existing `aria-live`/`role="status"` behavior when changing
  dynamic content.
- Respect `@media (prefers-reduced-motion: reduce)` for any new animation or transition.
