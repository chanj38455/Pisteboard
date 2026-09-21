# Piste Board (standalone)

A standalone clone of the Piste Board Claude Artifact — a weekly timetable
with fixed work hours, a ski-conditioning gym/dinner plan, work tasks with
due dates, and an Ask-Claude prompt bar that replans any week (or standing
rules spanning many weeks) on request.

This version has no dependency on the Claude Artifact runtime:

- **Storage**: all weeks, tasks, standing rules and settings are saved to
  the browser's `localStorage`. Nothing leaves your machine except the
  Ask-Claude requests below.
- **Ask-Claude**: instead of the Artifact `window.claude` sampling API, this
  calls the Anthropic Messages API directly from the browser using your own
  API key, with the `anthropic-dangerous-direct-browser-access` header
  Anthropic provides for exactly this kind of client-only app.

## Setup

1. Open `index.html` in a browser. Because it makes cross-origin requests
   to `api.anthropic.com`, some browsers block that from a plain `file://`
   page — if Ask-Claude requests fail immediately, serve the folder locally
   instead, e.g.:
   ```
   npx serve .
   ```
   or
   ```
   python -m http.server 8000
   ```
   and open the printed `http://localhost` URL.
2. Click the ⚙ button in the top bar and paste in an Anthropic API key
   (from console.anthropic.com). Pick a model — Sonnet 5 is the default and
   recommended balance of quality and cost; Haiku 4.5 is faster/cheaper,
   Opus 5 is the most capable.
3. Use the composer at the bottom to ask for a plan ("plan gym for ski prep
   next week", "I'm off work next Friday", "no more gym once ski season
   starts"), or tap any block to save notes, look up a how-to/recipe, or
   manage work tasks.

## Security note

The API key is stored in plaintext in this browser's `localStorage` and is
sent directly from your browser to Anthropic on every Ask-Claude request —
there is no backend. Anyone with access to this browser profile (or able to
inspect its network traffic) can read the key. Don't use this on a shared
or public computer, and treat the key like any other credential (rotate it
if you ever suspect it leaked).

## Files

- `index.html` — the entire app (HTML/CSS/JS, no build step, no dependencies
  beyond Google Fonts and the Anthropic API).
