# `remy` — Chronological Engineering Commit Ledger

> *The Chef — Autonomous Kitchen & Multi-Platform Order Desk*
>
> **Privacy Policy:** Source code internals and environment configurations live in the private engine repository. This public ledger records the chronological engineering milestones, architectural changes, and verification steps.

| Timestamp (UTC/Local) | Milestone / Commit Summary |
| :--- | :--- |
| `2026-10-28 11:33:16` | `chore: initialize remy-desk local CDP order ledger and package manifest` |
| `2026-10-28 14:16:32` | `feat(diet): add deterministic pescatarian ingredient classifier and meat/poultry flags` |
| `2026-10-28 14:24:29` | `feat(schedule): add T-60 quote and T-40 staging timetable scheduler` |
| `2026-10-28 14:28:06` | `feat(mail): add transactional order receipt parser stub` |
| `2026-10-28 14:32:36` | `infra(launchd): add KeepAlive plists for remy-desk serve (:8790) and watch loop` |
| `2026-10-28 19:34:40` | `feat(server): serve local JSON API and initial order desk dashboard on 127.0.0.1:8790` |
| `2026-10-28 21:19:59` | `style(ui): align order desk typography and panel grid with household shell` |
| `2026-10-28 21:20:57` | `feat(platforms): parallel CDP tab fan-out for Deliveroo, Just Eat, and Uber Eats quotes` |
| `2026-10-28 21:27:21` | `style(dashboard): compact quote cards and explicit approval cap badges` |
| `2026-10-28 21:29:55` | `feat(watch): background order-page poller with 20s in-flight courier cadence` |
| `2026-10-28 21:39:10` | `test(gate): enforce hard SQLite approval token boundary before checkout staging` |
| `2026-10-29 01:53:55` | `feat(ledger): backfill historical platform receipts into SQLite deliveries table` |
| `2026-10-29 02:45:12` | `feat(ready): add time-of-day daypart engine and preference-ranked Right Now slots` |
| `2026-10-29 03:02:35` | `test(ready): verify daypart slot ranking and dietary filter coverage` |
| `2026-10-29 03:17:25` | `fix(justeat): handle dynamic restaurant availability and ETA extraction` |
| `2026-10-29 14:08:40` | `feat(dispenser): add one-tap standing coffee order dispenser with cap guard` |
| `2026-10-29 14:10:00` | `test(dispenser): add unit harness for standing coffee order state transitions` |
| `2026-10-30 08:56:53` | `feat(shell): link shared shell.css and support embedded iframe mode for hub` |
| `2026-10-30 10:15:55` | `fix(browser): attach to persistent local Chromium CDP profile without tab leaks` |
| `2026-10-30 10:23:35` | `feat(reorder): implement native platform Order Again staging with price-cap verification` |
| `2026-10-31 13:58:49` | `feat(map): bundle local Leaflet courier map for live in-flight delivery tracking` |
| `2026-10-31 19:04:17` | `style(ui): refine in-progress courier telemetry strip and map viewport` |
| `2026-11-01 15:51:09` | `docs(readme): document CLI workflows, approval boundary, and basket lifecycle` |
| `2026-11-02 06:41:22` | `fix(track): normalize courier coordinates and terminal delivery states across platforms` |
| `2026-11-02 15:56:18` | `refactor(copy): cut dashboard word density by 49% (3,987 to 2,021 words); move prose to tooltips` |
| `2026-11-02 16:55:12` | `style(tables): show only delta state in rotation rows (closed, opens-at, ETA, fee)` |
| `2026-11-02 18:06:02` | `feat(ocado): add grocery product search and basket staging adapter` |
