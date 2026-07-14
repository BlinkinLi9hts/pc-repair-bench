# PC Repair Bench Assistant — Workflow Spec

## Concept
A hands-free, voice-to-text collaborative repair workflow. Technician narrates symptoms and findings; Claude (Jarvis) provides real-time component identification, research, validation, and next-step guidance. A browser-based checklist tracks progress per session on a bench monitor.

---

## Repo Structure

```
pc-repair-bench/
├── index.html          # Main checklist app (self-contained)
├── PC_REPAIR_SPEC.md   # This file
├── README.md           # Setup and deployment instructions
├── JARVIS.md           # Session-start context for Claude
└── sessions/           # Exported session logs (JSON / TXT)
```

Host on GitHub Pages for zero-dependency access from any bench device.

---

## Confirmed Bench Inventory (as of 2026-07-14)

### Display & Interface
| Item | Model | Notes |
|------|-------|-------|
| Bench monitor | KOORUI | Wall-mounted, arm-adjustable |
| Webcam / soundbar | Integrated | Mounted top of monitor |
| USB hub | ORICO | Docked to monitor bezel, 2x USB-A 3.0 |

### Soldering & Rework
| Item | Model | Notes |
|------|-------|-------|
| Soldering iron station | LONOVE 926 LED III | Orange, rotary dial, LED temp display |
| Rework / desoldering station | WEP 948D I | 3-ch preset, desoldering gun + iron, LCD |
| Anti-static work mat | KSLA | Wall-mounted behind bench |
| PCB holder / helping hands | Gooseneck alligator arms | On bench |
| Magnifying lamp | Arm-mounted | Far right bench position |
| Flux | Squeeze bottles | In orange parts bins |
| Solder | Spool (lead-free visible) | On LONOVE station |

### Measurement & Diagnostics
| Item | Model | Status |
|------|-------|--------|
| Multimeter | TBD — **NEEDED** | On shopping list |
| ESR meter | MESR-100 V2 (recommended) | **NOT YET PURCHASED** |
| Bench PSU | KORAD KA3005P or RD6006 (recommended) | **NOT YET PURCHASED** |
| CH341A BIOS programmer | + WSON-8 clip adapter | **NOT YET PURCHASED** |

### Network & Cable Testing
| Item | Model | Notes |
|------|-------|-------|
| Network cable tester | KOLSOL AT278 | In left field kit pouch |
| RJ45/RJ11 cable tester | With remote unit | In right field kit pouch |
| Tone probe / toner | 2x units | In left field kit pouch |
| Punchdown tool | — | Right pouch |
| Wire stripper | Yellow handle | Right pouch |

### General Tools
| Item | Model | Notes |
|------|-------|-------|
| Cordless drill | FISCHER | Pegboard |
| Screwdriver set | Multiple handle types | Pegboard |
| Precision bit kit | Craftsman | Red case, pegboard |
| Rubber mallet | — | Pegboard |
| Hammer | — | Pegboard |
| Flush cutters / scissors | — | Pegboard |
| DeWalt battery charger | — | Upper right pegboard |
| Power strip | Vertical mount | Right side pegboard |

### Organization
| Item | Notes |
|------|-------|
| Orange parts bins | 6+ along bench rail |
| Pegboard wall system | Full bench width |
| Left shelf | Tapes, adhesives, consumables |

---

## Shopping List (Priority Order)
1. **Multimeter** — Fluke 117 (preferred) or AstroAI AM33D (budget)
2. **Bench PSU** — KORAD KA3005P (30V/5A) or RD Tech RD6006 (60V/6A)
3. **ESR meter** — MESR-100 V2
4. **CH341A programmer** + WSON-8 clip adapter (for BIOS work)

---

## Active Repair Queue

| # | Device | Issue | Status |
|---|--------|-------|--------|
| 1 | Intel NUC5i5RYB | No power / will not POST | Triage pending — Session 2 |

---

## Checklist Tiers

### Tier 1 — Intake
- [ ] Client / owner description of problem: symptom, onset, precipitating event
- [ ] Visual inspection: physical damage, cracks, bent pins, missing components
- [ ] Burn marks or scorching on board, cables, or connectors
- [ ] Bulging, leaking, or discolored capacitors
- [ ] Smell test: ozone, burnt plastic, electrical burning
- [ ] Prior repair history documented
- [ ] Photo documentation taken (full board + problem areas)

### Tier 2 — No-POST Triage
- [ ] Reduced to minimal boot config: 1 RAM stick, no GPU, no storage
- [ ] Breadboard test: board removed from case, on non-conductive surface
- [ ] Internal speaker / POST buzzer connected and audible
- [ ] POST codes or beep codes documented
- [ ] Diagnostic LED codes documented (if motherboard has Q-LED/Dr. Debug)
- [ ] Front panel header (PWR_SW, RST_SW) verified or bypassed
- [ ] Boot attempted with known-good PSU

### Tier 3 — Power Delivery
- [ ] PSU standalone test (paperclip/jumper across PS_ON and GND on 24-pin)
- [ ] PSU fan spins under standalone test
- [ ] ATX 24-pin connector fully seated
- [ ] CPU EPS 4-pin or 8-pin connector connected and seated
- [ ] 12V rail measured (target: 11.4–12.6V)
- [ ] 5V rail measured (target: 4.75–5.25V)
- [ ] 3.3V rail measured (target: 3.135–3.465V)
- [ ] VRM area inspected: inductors, capacitors, mosfets
- [ ] PCIe power connectors verified (if GPU present)

### Tier 4 — Component Isolation
- [ ] Each RAM stick tested individually in slot A2
- [ ] All RAM slots tested with known-good stick
- [ ] GPU removed; tested with integrated graphics if available
- [ ] All storage (SATA + NVMe) disconnected
- [ ] All PCIe expansion cards removed
- [ ] All USB devices and non-essential peripherals disconnected
- [ ] CMOS cleared via jumper (bridge 10 sec, restore)
- [ ] CMOS battery removed 5+ min if jumper unavailable
- [ ] Known-good CPU tested if available

### Tier 5 — Board-Level Diagnostics
- [ ] Capacitors tested with ESR meter
- [ ] Suspected shorted capacitors identified (continuity / diode mode)
- [ ] Short-circuit detection via current-limited bench PSU
- [ ] Voltage rails probed at test points
- [ ] Clock signal confirmed (oscilloscope if available)
- [ ] BIOS chip identified: package type, manufacturer, part number
- [ ] BIOS chip read and backup created (CH341A programmer)
- [ ] BIOS reflash attempted with known-good image
- [ ] Trace inspection under magnification: cold joints, lifted pads, cracked traces
- [ ] Reflow suspected joints (WEP 948D I hot air)

---

## Voice-to-Text Workflow

1. **Open checklist** on KOORUI bench monitor
2. **State the intake** — device make/model, symptoms, history
3. **Share photo** via phone → Claude identifies board, flags known issues
4. **Work through tiers** — narrate findings, Claude responds with next step or research
5. **Check items off** as confirmed
6. **Export session** when done (TXT or JSON)

---

## Jarvis Behavior Guidelines

### Session Start
- Ask for device make/model if not stated
- Pull known failure modes and service bulletin if available
- Confirm which diagnostic tools are available for this specific job

### During Troubleshooting
- Always suggest least invasive test first
- State expected measurement values **before** technician probes (no anchoring after)
- Flag when a finding changes the working hypothesis
- Keep responses concise — technician has hands on hardware
- Call out **STOP** moments before any irreversible action (reflow, chip swap, trace repair)

### Research Role
- Part number lookups and substitutes
- Datasheet and pinout retrieval
- Known failure modes for specific models
- Capacitor specs (value, voltage rating, ESR range)
- BIOS chip identification and image sources

### Validation Role
- Confirm voltage readings are within tolerance before proceeding
- Cross-check symptom pattern against known failure modes
- Second opinion before committing solder

---

## Backlog
- Component lookup widget (part number → datasheet fetch)
- Photo annotation (markup damage locations)
- Repair cost estimator
- Parts order tracker
- Claude API integration for in-app AI suggestions (high priority)
