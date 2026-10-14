# AI Mentor — Project Brief

_Last updated: 2026-09-24_

## What the product is

AI Mentor is a personalized learning platform. The user states a goal, their current level and how much time they have. The AI then builds a learning **roadmap** of stages and tasks, and the platform guides the user through it, tracks their progress, and gives mentor-style guidance along the way.

It works in any field: programming, design, marketing, languages, career switching and more. It's bilingual, in **Arabic (RTL, the default)** and **English (LTR)**.

**Core flow:** goal → level and time → AI generates a roadmap → the user completes tasks → progress is tracked → the mentor guides → the AI proposes adaptations → the user accepts or rejects them.

**Repos:** this repo is the frontend (Next.js 16, App Router, Tailwind v4, Redux Toolkit / RTK Query, next-intl). The backend is a separate Laravel 12 REST API built by another developer. The contract between them is in `API_CONTRACT.md`.

## Design

- **Style:** clean and calm "Adaptive Intelligence" look, with light and dark themes. The source of truth is `design.md`.
- **Colors:**
  - Primary: deep navy `#12314D`.
  - Secondary: blue `#1D4E89` / `#4683CB`.
  - Accent: purple `#7C3AED`, used only for the active milestone or current task.
  - Page canvas: `#F8FAFC`; hero background: midnight `#0A1930`.
- **Shapes:**
  - Cards and panels: 16px radius.
  - Icon boxes: 12px radius.
  - Inputs and buttons: 8px radius.
  - Status tags and chips: fully rounded pills.
- **Fonts:**
  - English: Space Grotesk for body and UI, Nunito Sans for display headings.
  - Arabic: Zain for large headings (`h1`/`h2`) and Noto Sans Arabic for everything else. These are on PR #34, not yet merged.
- **Motion:** subtle reveal and fade-in animations (Framer Motion / GSAP), with an animated heading-reveal on marketing headings.
- **Rule:** every screen must work in RTL and LTR, and at mobile and desktop widths.

## What exists today

**Home page (marketing):** Hero, How it works, Features, Pricing and FAQ sections, plus a final call-to-action. Pricing has two plans: Free, which is available, and Pro, marked "Coming soon".

**Auth page:**
- Sign in and create account, connected to the real API.
- Tokens are kept in memory only, with an automatic refresh.
- A side brand panel that changes its copy between sign-in and register.
- "Forgot password" and "Sign in with Google" are shown, but each gives an honest "not available yet" message.

**Onboarding:** a multi-step wizard covering field/domain, skill level, time commitment, success goal and learning preferences, followed by a review step. It saves the user's preferences and learning profile to the API.

**Dashboard:**
- An app shell with welcome, progress, continue-learning, today's focus, mentor insight and recent activity sections.
- Starts AI roadmap generation (duplicate-safe), polls until it's ready, then shows the roadmap as stages and tasks.
- Sections the backend doesn't provide data for yet show honest "unavailable" or empty states instead of fake data.

**Foundations:**
- Arabic and English with RTL and LTR.
- Light and dark theme.
- One consistent error model shared across the API layer.
- Unit and component tests (Vitest + MSW) and e2e tests (Playwright).

## What's missing (against the MVP)

- **Task actions:** "Mark complete" and "Skip" appear but are disabled, because there's no backend endpoint yet.
- **Progress data:** real progress tracking, streaks and achievements.
- **AI mentor:** mentor chat, AI insight, and adaptation proposals (accept or reject).
- **Learning resources:** discovering and validating resources for each task.
- **Roadmap changes:** regenerate, reset, and change goal (then rebuild the roadmap).
- **Dashboard data:** current lesson, today's focus tasks and recent activity. These wait on backend data models.
- **Account features:**
  - password recovery (no backend yet)
  - Google sign-in
  - a profile/settings page
  - account deletion
- **Paid Pro plan:** out of MVP scope, since payments are excluded.

Explicitly **out of MVP scope:**
- multiple active roadmaps
- payments
- community and social features
- reminders and calendar scheduling
- native mobile apps
- enterprise SSO

## Work in progress and known gaps

- **PR #34** (`feature/arabic-fonts`): the new Arabic fonts plus a line-spacing fix for wrapped Arabic headings. Open and waiting for review.
- **Branch `feature/auth-register-brand-copy`:** separate copy for the register side panel, plus updated sign-in text. Committed locally, not pushed yet.
- The English fonts still load from Google Fonts, so the build needs network access.
- Parts of `docs/` are outdated. For example, `docs/00-project-overview.md` still says there's no API client and no tests.
