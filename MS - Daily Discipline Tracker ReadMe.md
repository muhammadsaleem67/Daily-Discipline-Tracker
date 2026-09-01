# Daily Discipline Tracker — Feature Guide

A single-file HTML app for tracking a daily routine (prayers, study, school,
exercise, courses) with streaks, analytics, and now a few "coach-like"
features. Everything runs client-side; data is saved via the app's built-in
storage, per-user, in your browser.

## Today tab

- **Phased checklist** — tasks grouped into phases (Morning, Study block,
  School, Afternoon, Evening, Wind down), each shown with its time.
- **"Now" highlighting** — the task matching the current time is visually
  marked so you always know what you should be doing.
- **N/A per task** — mark a task as not applicable for the day (e.g. no
  school on a holiday) without breaking your streak math.
- **Prayer-time-aware scheduling** — Fajr/Maghrib/Isha tasks pull their time
  from your Settings prayer times instead of a fixed clock time.
- **Streak tracking** — current streak and best-ever streak, with automatic
  reset if a day is fully missed.
- **Milestone badges** — a banner appears at 7, 30, 100, and 365-day streaks.
- **Evening warning banner** — if it's after 8 PM and you're not done,
  you get a nudge referencing your current streak.
- **Pause day** — for sick days or travel; the day is excluded from streaks
  and averages instead of breaking them.
- **Daily notes** — free-text field for anything worth remembering.
- **🎙 Voice notes (NEW)** — dictate your daily note using your browser's
  speech recognition instead of typing. Falls back to disabled if your
  browser doesn't support it.
- **Risk score card (NEW)** — each morning, a quiet dial estimate of how
  likely today is to be an "off day," blended from your historical
  performance on this specific weekday and your last two weeks overall.
  Only appears when there's enough history and the risk is meaningful.
- **Quote of the day** — a deterministic quote tied to the date.
- **Backup reminder banner** — nudges you to export your data if it's been
  30+ days since your last export.
- **Reset today** — clears today's checkboxes without touching streak data
  from prior days.

## Insights tab

- **7-day / 30-day completion stats**, plus best streak.
- **Monthly heatmap** — calendar view, color-coded by completion %, with
  month navigation and a "today" outline.
- **Most-skipped tasks** (last 30 days) — ranked list of what you avoid most.
- **Consistency by task** (last 30 days) — ranked list of your weakest
  tasks by completion rate.
- **Trend** — this month vs. last month completion %, plus a sparkline.
- **Sleep/consistency correlation box** — a written observation about how
  your patterns relate.
- **Look up any date** — pull up any past day's full checklist, notes, and
  completion %.
- **Weekly reflection (NEW, AI-powered)** — a "Generate" button sends your
  last 7 days of completion data, missed tasks, and notes to Claude, which
  writes a short, honest, non-fluffy paragraph on patterns and one concrete
  suggestion for the coming week.
- **Printable monthly report (NEW)** — builds a clean, printer-friendly
  summary (streak, best streak, month average, a day-by-day completion
  table) and opens your browser's print dialog so you can save it as a PDF
  — useful to show a mentor, tutor, or for a personal portfolio.

## Courses tab

- **Long-term course/goal tracker**, separate from the daily routine —
  add a course with a total unit count (e.g. "40 modules"), then increment
  progress with +/− buttons. Shows a progress bar and %.

## Settings tab

- **Theme picker** — four color themes (default, ocean, forest, plum).
- **Prayer time configuration** — update Fajr/Maghrib/Isha as they shift
  through the year; all prayer-linked tasks update automatically.
- **Task editor** — add, reorder (up/down), and delete tasks; set each
  task's time, phase, and day-scope (every day / weekdays / weekends).
- **Compact daily view (NEW)** — a toggle that switches the Today tab to a
  condensed mode: hides the quote, banners, times, risk card, and notes
  box, leaving just a fast tap-through checklist for a 30-second morning
  check.
- **Backup / restore** — export your full history, streaks, tasks, and
  settings as a JSON file; import it back on this or another device/browser.

## What's genuinely "advanced" here (and what isn't)

To be transparent about the newest additions:

- The **weekly reflection** makes a real API call to Claude and will only
  work while the app is open inside an environment that provides that API
  access (e.g. as a Claude-hosted artifact). It is not a local/offline
  feature.
- The **risk score** is a simple statistical estimate (a blend of your
  historical same-weekday and recent 2-week completion rates) — not a
  trained predictive model. It's meant to be a quiet, honest signal, not a
  guarantee.
- **Voice notes** depend on the Web Speech API, which isn't supported in
  every browser (Chrome-based browsers work best; some Firefox/Safari
  versions won't).
- There is **no live shareable link** — that would require a backend
  server this app doesn't have. The closest equivalent right now is the
  printable report or the JSON export, either of which you can hand to
  someone else.

## Honest note

This app already has a lot in it. If you're not opening it daily yet, more
features won't fix that — worth trying the current version for a week
before adding anything else on top of tonight's additions.

## Round two: reminders, geolocation, auto-reschedule, charts, focus mode

- **Task reminders (notifications)** — a Settings toggle that requests
  browser notification permission and fires a native notification when a
  task's time arrives. **Caveat:** this only works while the tab stays
  open — a single HTML file with no backend can't push notifications when
  the browser is closed or the tab is in the background on mobile. A true
  "notify me even when the app is shut" feature needs a real server and a
  installed PWA/service worker, which is out of scope for a single file.
- **Location-based prayer times** — an "Auto-fill from my location" button
  in Settings that uses your browser's geolocation and a free public
  prayer-time API (Aladhan) to fill in Fajr/Maghrib/Isha automatically
  instead of manual entry. You can still edit them by hand afterward.
- **Auto-reschedule suggestion** — if a task has been missed 3+ times in
  the last 7 days, a banner offers to ask Claude for a better time slot
  (checked against your other fixed tasks), with a one-click apply. You
  can also dismiss it, which won't ask again for that task this week.
- **Trend chart (Chart.js)** — a proper line chart of your last 14 days'
  completion %, alongside the existing sparkline and heatmap.
- **Focus mode** — a "Focus" button appears on whichever task is currently
  "now." It opens a full-screen 25-minute countdown with pause/resume, and
  notifies you (if reminders are on) when time's up.

### What I deliberately did not build, and why

- **Multi-device sync via login** — this needs real backend
  infrastructure (auth, a database, a server) that a single HTML file
  fundamentally can't provide. The closest available option is still the
  JSON export/import already in Settings.
- **Gamification (points, levels, leaderboards)** — I flagged this as
  actively risky for a discipline habit, since it tends to shift
  motivation from internal to external and collapses once the novelty
  fades. Left out on purpose.
- **Social/competitive streak comparison** — same reasoning; turns a
  private practice into a performance. Left out.
- **More AI-generated pep talks/affirmations** — the app already has one
  AI feature (the weekly reflection). Stacking more AI text on top adds
  noise, not discipline. Left out.

