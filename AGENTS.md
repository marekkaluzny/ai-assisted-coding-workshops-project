# AGENTS.md

## Project overview

Kainos Task List — a training template for an AI-assisted coding workshop. It's a
plain **HTML/CSS/JavaScript** browser app (no framework, no bundler, no build step).
The app ships with most logic left as empty function stubs annotated with
`// TODO Task N: ...` comments; workshop participants implement them incrementally
across 5 tasks (localStorage persistence, done/delete, filtering, due dates, AI
priority suggestions via the OpenRouter API).

See [README.md](README.md) for the full workshop plan and prerequisites.

## Project structure

| File | Purpose |
|---|---|
| [index.html](index.html) | Main page — full task list UI, all CSS inlined in a `<style>` block |
| [popup.js](popup.js) | Application logic — state, persistence, rendering, event wiring |
| [options.html](options.html) | Settings page — OpenRouter API key input, CSS inlined |
| [options.js](options.js) | Settings logic — load/save the API key |

There is no `package.json`, no npm scripts, and no test suite in this repo.

## Dev environment / running the app

- No install step is required (no `npm install`, no bundler).
- Open [index.html](index.html) directly in a browser, or right-click it in VS Code
  and choose **Open with Live Server** for auto-reload.
- After every code change: save the file and refresh the browser tab.
- Debug with browser DevTools (F12) → Console tab. There is no build/compile step
  to watch for errors — syntax errors surface only at runtime in the console.

## Testing instructions

- There is no automated test suite (no Jest/Vitest/etc. configured).
- Validate changes manually in the browser: reload the page, exercise the UI
  (add/toggle/delete tasks, filters, due dates, AI suggestions), and check the
  DevTools console for errors.
- Do not add a test framework or build tooling unless explicitly asked — this is
  intentionally a zero-install, static workshop project.

## Code style guidelines

- Vanilla JS, no frameworks/libraries, no TypeScript, no modules (`<script>` tags
  loaded directly).
- 2-space indentation, single quotes, semicolons.
- Keep the existing section-divider comment style, e.g.:
  ```js
  // ── Persistence ────────────────────────────────────────────────
  ```
- State lives in a single top-level `state` object in [popup.js](popup.js); read
  and mutate it through the existing functions rather than introducing new global
  state.
- Preserve `// TODO Task N: ...` comments for stubs that belong to a task the user
  hasn't asked you to implement yet; only fill in stubs relevant to the requested
  task.
- Keep CSS inline in the `<style>` block of the relevant HTML file (matches the
  existing pattern) rather than extracting a separate stylesheet, unless asked.

## Security considerations

- The OpenRouter API key entered on the settings page ([options.html](options.html)
  / [options.js](options.js)) is stored in `localStorage` and used client-side only
  — never hardcode API keys or commit real keys/secrets into source files.
- When rendering user-provided text (task titles, etc.) into the DOM, avoid
  introducing `innerHTML` injection issues — escape or sanitize user input before
  interpolating it into HTML strings, consistent with how existing rendering code
  handles todo text.
- Any calls to the OpenRouter API must go over HTTPS and must not log or expose
  the API key (e.g., in console output or error messages).

## Keeping this file up to date

- Whenever a change is significant — new/removed/renamed files, new dependencies
  or tooling, changes to how the app is run/tested, or new coding conventions —
  update the relevant section(s) of this AGENTS.md in the same change.
- Small, local edits that don't affect structure, dependencies, or conventions
  (e.g. filling in a single `TODO Task N` stub as intended) do not require an
  update.
