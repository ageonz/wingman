# Wingman — ASAP Tickets Contact Center CRM

Wingman is a single-file, zero-backend CRM console for travel-agency call centers.
It runs entirely in the browser (Alpine.js 3 + Tailwind + Chart.js + FontAwesome
via CDN) and persists all data locally through a sandbox-safe localStorage wrapper.

## Builds

| File | Purpose |
|---|---|
| `index.html` (public build, a.k.a. wingman.html) | Deployed to GitHub Pages. No admin/GitHub UI at all. |
| `admin/wingman-Q-admin.html` | Admin "Q" build — identical app PLUS the GitHub Publishing panel, visible only when signed in with role `admin` (email local part containing "admin" or "q"). Recommended to keep this file OFF GitHub, on the admin machine only. |

## Features

- **Mock Gmail login** — regex-validated email, 6+ char password, remember-me, demo mode
- **Team Roster** — upload/paste the backoffice "Agent List (New)" export; email-anchored
  parser extracts agents, ext, direct numbers, teams, offices and supervisors; dedupes,
  skips report junk lines; searchable + filterable; supervisor grouping with agent counts
- **Grammar Coach** — offline rule engine today (grammar, periods/commas, capitalization,
  spelling, quality score 0–100); Qwen API fully wired behind `AI_CONFIG.useLiveAPI`
- **Shift Clock** — Clock In / Pause / Clock Out, per-bucket timers (online/paused/break/lunch),
  survives refresh, shift history, CSV export; no idle auto-detection by design
- **Live Chat + Macros** — seeded conversations, 16 macros with {{variable}} replacement,
  simulated passenger replies, resolve flow, unread badges
- **Call Log & KPI** — call counter with reset, auto Call IDs (CALL-YYYYMMDD-XXXX),
  lead links, 13-type hardcoded point system (Inquiry 1 … Agency compensation 18)
- **Hold Timer** — loud Web Audio siren at zero (no audio files), keeps counting across
  pages, Stop Alarm control, expired banner
- **Fare Difference Calculator** — integer-cent engine, 24 non-refundable tax codes with
  automatic recollection, GDS pricing parser, self-test 3/3 ($125.00 / $246.60 / $167.60)
- **Knowledge Base** — GDS commands (Apollo/Galileo/Sabre/Amadeus), tax reference,
  fare glossary, IATA codes, SOPs, training modules
- **Name Correction Policies** — 15 airlines with fees, docs, GDS commands, trade desks,
  and side-by-side comparison
- **Performance** — points by case type, team leaderboard charts
- **Templates** — Passenger / Internal / Both categories with signature & metadata wrapping

## Run locally

1. Clone this repo (or download `index.html`).
2. Open `index.html` directly in a browser, or serve the folder (`npx serve .`).
3. Sign in with any valid email + 6-char password, or use demo mode.

## Publish workflow (admin)
