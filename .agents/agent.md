# AI Agent Guidelines - Sol Spy

This document serves as a developer guide for AI coding assistants working on the **Sol Spy** codebase.

## Developer Rules & Standards

### 1. Astro Dev Server
Always run the dev server in the background as specified by the project rules:
```bash
astro dev --background
```
Use `astro dev status` to check if it's running, and `astro dev logs` for terminal feedback. Never run standard blocking `astro dev`.

### 2. Styling & UI Design
- **Dark Theme Priority**: The UI must look like a high-end, premium cyberpunk terminal or financial dashboard. Use `bg-slate-950` as the main body background.
- **Tailwind Version**: Tailwind CSS v4.x is configured via `@tailwindcss/vite`. Import stylesheet using `@import "tailwindcss"` in `src/styles/global.css`.
- **Interactive States**: Use hover effects and transitions. Active indicators must pulse, and interactive buttons should shrink slightly when clicked (`active:scale-95` or `active:scale-[0.99]`).

### 3. JavaScript Standards
- No client framework (React, Vue, etc.) unless requested. Maintain raw Vanilla JavaScript inside `<script>` blocks inside Astro templates.
- Write robust error boundaries around API fetches. If the API returns invalid objects, fall back to showing a styled offline/error card rather than throwing uncaught errors that break the Mini App context.
