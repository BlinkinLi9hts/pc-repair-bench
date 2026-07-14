# PC Repair Bench Assistant

A hands-free, browser-based troubleshooting checklist for collaborative PC repair sessions with Claude (Jarvis).

## Workflow

```
State the intake (voice-to-text)
→ Share a photo — Claude identifies the board, flags known issues
→ Work through tiers — narrate findings, Claude responds with next steps
→ Check off items as confirmed
→ Export session log when done
```

## Usage

1. Open the [live checklist](https://BlinkinLi9hts.github.io/pc-repair-bench/) on the bench monitor
2. Enter device name and chief complaint
3. Work through Tiers 1–5 with Claude
4. Export session as `.txt` or `.json` when done

No server. No dependencies. Works offline after first load.

## Files

| File | Purpose |
|------|---------|
| `index.html` | Self-contained checklist app |
| `PC_REPAIR_SPEC.md` | Full workflow spec, inventory, and backlog |
| `JARVIS.md` | Session-start context doc for Claude |
| `README.md` | This file |
| `sessions/` | Exported session logs (gitignored or kept locally) |

## Checklist Tiers

| Tier | Focus |
|------|-------|
| 1 — Intake | Visual inspection, history, photos |
| 2 — No-POST Triage | Minimal boot, breadboard, POST codes |
| 3 — Power Delivery | PSU, rail voltages, VRM |
| 4 — Component Isolation | RAM, GPU, storage, CMOS |
| 5 — Board-Level | Capacitors, traces, BIOS chip, reflow |

## Deployment (GitHub Pages)

1. Push this repo to GitHub
2. Settings → Pages → Deploy from branch `main` / root
3. Live at: `https://BlinkinLi9hts.github.io/pc-repair-bench/`

## Bench Setup

See `PC_REPAIR_SPEC.md` for full confirmed tool inventory and shopping list.

**Key equipment:**
- LONOVE 926 LED III — soldering iron station
- WEP 948D I — desoldering gun + rework station
- KOORUI monitor (wall-mounted) + ORICO USB hub
- KOLSOL AT278 network tester

**Pending (shopping list):**
- Multimeter (Fluke 117 recommended)
- Bench PSU (KORAD KA3005P or RD6006)
- ESR meter (MESR-100 V2)
- CH341A BIOS programmer + WSON-8 clip

## Roadmap

- Claude API integration for in-app AI suggestions
- Component lookup widget (part number → datasheet)
- Photo annotation / markup
- Parts order tracker
- Repair cost estimator
