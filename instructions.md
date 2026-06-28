# Instructions for Claude Code

This file gives context for working on this project in VS Code. Read this before making changes.

## What this project is

A single-file personal time tracking web app (`index.html`, also distributed as `time-tracker.html`). It is meant to be hosted as a static page (currently via GitHub Pages) and installed on iPhone via Safari's "Add to Home Screen", so it behaves like a small PWA.

There is no build step, no package manager, no framework. Everything (HTML, CSS, JS) lives in one file on purpose. Keep it that way unless the user explicitly asks to split it into multiple files or add tooling.

## Hard constraints, do not break these

- **Single file.** All CSS and JS stay inline in the one HTML file. No external dependencies, no CDN imports, no build process.
- **No backend.** All data lives in `localStorage` under the key `timeTrackerData_v1`. There is no server, no API calls, no analytics.
- **iOS Safari is the primary target.** Test changes mentally against iPhone Safari behavior: viewport-fit, safe-area insets, the `apple-mobile-web-app-capable` meta tags, and `navigator.clipboard` with the `execCommand` fallback for copy actions must keep working.
- **English only in code.** All code, comments, and identifiers must be in English, regardless of what language the user writes in chat.
- **No em dash, anywhere.** Not in UI copy, not in code comments, not in this file's prose if it's user-facing. Use commas, parentheses, or "to" instead. This is a strict personal preference of the user.
- **Light, minimal, clean design.** No dark mode, no flashy animations. Big, thumb-friendly buttons. Sans-serif system font for body text, monospace for all time and hour values (this is the deliberate design signature, keep it consistent if you add new time-related displays).

## Data model

```js
{
  entries: [
    {
      id: "e_<timestamp>",
      date: "YYYY-MM-DD",
      clockIn: "HH:MM" | null,
      clockOut: "HH:MM" | null,
      breaks: [
        { start: "HH:MM" | null, end: "HH:MM" | null }
      ]
    }
  ]
}
```

- One entry per calendar date. Manual entry/edit logic merges into an existing entry for that date rather than creating duplicates.
- An entry with `clockOut: null` is "in progress" and is excluded from weekly hour totals.
- Hours are computed as `(clockOut - clockIn) - sum(break durations)`, handling overnight wraparound by adding 1440 minutes if the end time is earlier than the start time.
- Weeks are grouped Monday to Sunday. A week's total is the sum of completed entries' hours in that week. Over 40 hours triggers the overtime visual flag.

## Code structure inside the file

- `<style>` block: CSS variables under `:root` define the whole palette and spacing. Change tokens there, not by hardcoding new colors inline.
- `<script>` is a single IIFE, organized into labeled sections by comment headers: Storage, Date and time helpers, Hours calculation, Data access, Rendering (today card, weeks list), Copy summaries, Toast, Today actions (clock in/out, breaks), Modal (manual entry form), Wire up.
- Rendering is done by full re-render (`renderAll()` calls `renderToday()` and `renderWeeks()`) after every state change, not incremental DOM patching. Keep this pattern for consistency unless performance becomes an actual issue (it will not, given the realistic data volume of a personal time log).

## Known platform quirks to keep in mind

- Local `file://` access in iOS Safari does not reliably support "Add to Home Screen" or persistent storage. The supported deployment path is hosting with a real HTTPS URL (currently GitHub Pages). Do not suggest local-file-based workflows as the primary install method.
- Chrome on iOS cannot hide its browser toolbar like Safari can (no equivalent to Safari's standalone meta tag support). Safari is the canonical target browser for the "installed app" experience.
- `navigator.clipboard.writeText` requires a user gesture and can fail silently in some contexts, hence the `execCommand("copy")` fallback in `fallbackCopy()`. Keep both paths if touching the copy logic.

## Workflow preferences

- The user prefers handling one issue at a time. Do not expand scope or propose unrelated improvements unless asked.
- Prefer small, targeted diffs over rewrites. If a change can be made with a `str_replace`-style edit instead of regenerating the whole file, do that.
- If adding a feature changes the data model (`entries` shape), make sure old saved data in `localStorage` still loads without crashing (defensive checks, default values), since there is no migration mechanism and no backend to fall back on.