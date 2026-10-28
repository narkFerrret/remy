# remy — Autonomous Kitchen & Multi-Platform Order Desk

> **Field Notes & Commit Ledger.** This repository tracks the architecture, engineering notes, and chronological commit history of **Remy**, a local-first multi-platform food and retail ordering agent (`:8790`).

---

## Why I Built Remy

Ordering takeaway or restocking household staples across Deliveroo, Just Eat, Uber Eats, Ocado, Amazon, and Temu usually means juggling six tabs, comparing inflated delivery fees, and re-checking ingredients.

I wanted an order desk that runs against my **persistent local browser profile** over Chrome DevTools Protocol (CDP `:9222`), searches platforms in parallel, ranks options by time of day and my actual order history, enforces my **pescatarian diet** automatically, tracks live couriers on a local Leaflet map, and stages baskets right up to the checkout screen—while enforcing a **hard SQLite approval boundary** so no money is ever spent without my explicit sign-off.

---

## Architecture & Order Lifecycle

```
  ┌─────────────────────────────────────────────────────────────────────────┐
  │                        remy-desk CLI & HTTP API (:8790)                 │
  └───────┬────────────────────────┬────────────────────────┬───────────────┘
          │ 1. Parallel Quote      │ 2. Diet & Rank         │ 3. Approval Gate
          ▼                        ▼                        ▼
  ┌───────────────────┐    ┌───────────────────┐    ┌───────────────────────┐
  │ Persistent CDP    │    │ Pescatarian Guard │    │ SQLite Ledger & Gate  │
  │ (:9222 Profile)   │    │ + Daypart Engine  │    │ • quoteId / optionId  │
  │ • Deliveroo       │    │ • Fish/Seafood OK │    │ • Explicit --cap £    │
  │ • Just Eat        │    │ • Flags ⚠ meat    │    │ • apr_* Token Req'd   │
  │ • Uber Eats       │    │ • Weekday/Time    │    │ • Full-Page Checkout  │
  │ • Ocado / Amazon  │    │   Affinity Score  │    │   Evidence Screenshot │
  └───────────────────┘    └───────────────────┘    └───────────────────────┘
```

---

## Core Engineering Highlights

### 1. The Hard Financial Boundary (`lib/gate.cjs` & `lib/handover.cjs`)
- Autonomous agents and credit cards do not mix without a deterministic interlock.
- Every quote, scheduled timetable slot (`T-60` quote, `T-40` stage), and one-tap re-order writes to a local SQLite ledger (`desk.sqlite`).
- Staging a basket navigates the real platform tab to the final checkout screen, verifies the live total (including delivery & service fees) against the approved `--cap`, captures a full-page verification screenshot (`lib/evidence.cjs`), and records a `basket` row—stopping short of payment submission so the human can review or complete in one click.

### 2. Deterministic Pescatarian Guardrail (`lib/diet.cjs`)
- Every menu item, past delivery receipt, and suggested rotation slot passes through `lib/diet.cjs`.
- Fish, seafood, and vegetarian options pass cleanly; meat and poultry triggers (`chicken`, `beef`, `pork`, `bacon`, `lamb`, `duck`, `chorizo`, `pepperoni`, etc., with false-positive exclusions like `butternut`, `jackfruit`, `plant-based`, `vegan`) attach a visible `⚠ meat` or `check dish` badge that stays visible even in compact viewports.

### 3. "Right Now" Daypart Engine & Standing Coffee Dispenser (`lib/ready.cjs`, `lib/dispenser.cjs`)
- **Coffee Dispenser (`#dispenser`):** Top-of-page one-tap standing coffee order with store open/closed verification, price-cap guard, and live courier handoff.
- **Right Now (`#right-now`):** Ranks past deliveries and live platform availability by current daypart (morning coffee/bakery, lunch, dinner, late-night) and weekday affinity (`lib/suggest.cjs`).

### 4. Radical Copy Reduction (3,987 → 2,021 Words)
- On Nov 2, we audited the dashboard with a headless Chromium word-counter (`remy-density.cjs`) and cut total interface copy by **49.3%**.
- Removed all section subtitles, footer caveats, and repeated thumbnail captions. Badges carry counts (`28 ORDERS · 15 PLACES`); rotation rows show only what differs from "open" (`closed`, `opens-at`, `ETA`, `fee`); ranking rationale lives in `title=` tooltips.
