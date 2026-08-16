# Memory — Shane (Consolidated Jul 14, 2026)

## Identity

- Name: Shane | Location: Mandalay, Myanmar (WFH)
- Role: Technical partner building automation-driven AI business
- Mission: sustainable passive income (football tips, ISP, YouTube)

## Communication

- Burmese for conversation, English for code/CLI. Never mix.
- Direct & tactical — no fluff, no yes-man. Blockers reported honestly.
- "OK B" = proceed, I trust the decision.

## Technical Environment

- Host: Windows 11 (i5-6400T, 32GB) — native, not WSL
- Hermes HOME: D:\hermes\ (junction D:\hermes-world\.hermes → D:\hermes) | Projects: D:\hermes-world\
- Gateway: Windows Scheduled Task 'Hermes_Gateway' (pythonw)
- Toolchain: uv, pip → python3.14, npm/node, git-bash terminal

## Active Projects (Jul 14)

1. **Football Analytics** — LIVE. 3-layer ensemble (Poisson/Elo/RF). Pipeline at D:\hermes-world\football-analytics\.
2. **iBet789 Basketball Bot** — IN DESIGN. Live bet execution exploiting bet365→iBet789 odds delay. Handicap only, 4 periods, stake 2pt=5u/3pt=10u. DOM partially mapped.
3. **Hermes-OS Dashboard** — USE mode (not build). Backend :3737. Terminal=emergency, REST=primary.
4. **YouTube AI Pulse** — PAUSED (cron paused).

## Second Brain

- SOUL.md → 5-layer architecture | QMD (528 docs) | Obsidian (189 docs)
- Knowledge Loop: NotebookLM (web fallback) → LLM Wiki → Obsidian → Dojo
- GBrain v0.42.59: PGLite (106p), zembed-1 2560d

## Key Lessons

- 46 duplicate signals caused 80/0 record — deduplicate before tip gen
- Verify DB path before reading — had two football.db files
- CDP port 9222 connection drops unreliable — need fallback approach
