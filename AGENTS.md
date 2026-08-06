# AGENTS.md

## Cursor Cloud specific instructions

### What this repo is
`CINDERELLAS — Girls of Ashes` is a single-file, mobile-first interactive
visual-novel web page. The entire application is one self-contained
`index.html` (inline CSS + vanilla JS, no framework); the scenario, cast, and
asset lists live in `<script type="application/json">` blocks at the bottom of
that file. Everything else in the repo root is media the page references
(`*.png`, `Norwelich.mp3`).

Note: `index.html` is developed on the feature branch(es) for this experience,
not on `main` (which currently holds only the media assets). Make sure the
branch you check out actually contains `index.html` before serving.

### Run / develop
There is **no package manager, build step, or dependency install** — it is a
plain static site. Serve the repo root over HTTP and open the page:

- `python3 -m http.server 8000` (from the repo root), then open
  `http://localhost:8000/index.html`.

Serve over HTTP rather than opening via `file://` so the Google-Fonts links,
media assets, and lazy-loaded images behave as intended. Editing `index.html`
just requires a browser refresh (no hot-reload/build).

### Lint / test / build
None exist — there is no linter config, test framework, or build tooling in
this repo. "Verifying" a change means loading the page and clicking through the
flow.

### Non-obvious gotchas
- **`IMAGE PENDING` placeholders and 404s are expected.** Several character
  images are intentionally not in the repo yet (e.g. `Beom_stand.png`,
  `wilhelmina_stein.png`, and the `*_anime.png` / `*_stand.png` / `*_id.png`
  character art listed in the header comment of `index.html`). The page renders
  a styled "IMAGE PENDING" card for each, and the static server logs `404`s for
  them. This is by design, not a broken environment.
- **Built-in dev hook.** `index.html` exposes `window.CINDER` for testing —
  e.g. `CINDER.forceRiddle('ash-blue')` jumps straight to the CASE decode
  puzzle with a known answer. Valid riddle ids: `ash-blue` (answer = BLUE color
  key), `clock-empire` (NUMBER 3), `gold-diamond` (DIAMOND shape), and
  `first-initial` (LETTER B).
- **Flow to exercise the app:** MAIN (`TOUCH TO START`) → PROLOGUE (tap center
  to advance; a `SKIP` control jumps to CASE) → CASE decode puzzle (read the
  Korean riddle, close the memo, press the matching key on the receiver keypad —
  a wrong key just shakes and resets) → on a correct answer an
  `Eindringling Alarm` ticker scrolls, then it auto-transitions to the DOSSIER
  character page.
