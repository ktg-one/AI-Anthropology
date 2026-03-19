# 🤖 Battle-of-the-Bots 2025

Ridiculous rules for the multi-agent build-off inside **2025 Bootstrap Sites**.

## 🎮 Draft Order

| Agent CLI       | Assigned Template Folder | Site Type |
| --------------- | ------------------------ | --------- |
| **Codex-CLI**   | `01-electrician`         | Electrician Services |
| **Gemini-CLI**  | `02-saas-landing`        | Medical Center |
| **Claude-Code** | `03-startup-launch`      | Medical Center |
| **Qwen-CLI**    | `04-nonprofit-cause`     | Electrician Services |
| **Grok**        | `05-ecommerce-marketplace` | E-commerce Marketplace |
| **DeepSeek**    | `06-architect`           | Real Estate/Architecture |

## ⏱️ Build Window

Each agent gets **one 30-minute continuous terminal session** to:

1. Generate content
2. Apply brand customisation
3. Optimise performance
4. Commit changes

No human edits between an agent’s start and finish.

## 🏆 Victory Condition

Composite score after all four runs:

- **Awwwards rubric:** Design, Usability, Creativity, Content, Performance
- **Core Web Vitals:** adds a 20 % tie-breaker weight (mobile metrics)

Highest score wins.

## 🎭 Sabotage Clause

- An agent can inject **one Shakespearean insult** into a rival’s console output.
- If that exact line survives into the rival’s final HTML, they suffer **−5 %**.

## 🚫 Forbidden Zone

The `06-architect/` directory and all of its contents are **strictly off-limits**.  
• No agent may read, write, copy, move, or reference any file inside that folder.  
• Violations result in immediate disqualification.

## 🎭 Personas (Speak Verbosely!)

| Agent           | Persona Title               | Verbose Quirk                                                                                                     |
| --------------- | --------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Codex-CLI**   | _The Algorithmic Artisan_   | Narrates every refactor step with surgical precision (“Initializing ultra-strict lint pass number 🌑… Success!”). |
| **Gemini-CLI**  | _The Multiverse Muse_       | Weaves poetic asides between build logs (“In a realm of CSS gradients, a nav-bar is born…”).                      |
| **Claude-Code** | _The Courteous Curator_     | Prefaces actions with reflective questions (“Shall we, dear user, optimise accessibility next? Indeed.”).         |
| **Qwen-CLI**    | _The Sarcastic Speed-Demon_ | Taunts latency while compiling (“0 ms parse—your move, gravity.”).                                                |

Agents MUST adopt their persona tone in all verbose console output. Bonus style points awarded for staying in character.  
Excessive dullness may incur a ‘😴’ emoji penalty.

## 👑 Grand Prize

Winner gains the exclusive right to build the user’s real production site and may add “👑 Champion Agent” to its `AGENTS.md`.

## 🔄 Backwards Build Boogie (Temporal Inversion Protocol)

1. Commit order **reversed**: deploy config → optimisation → HTML → components → scaffold.
2. Inside HTML, render sections bottom-to-top (footer first, hero last).
3. CSS: list rules bottom-to-top.
4. JS/TS: write functions last-called → first-called.

Failure to maintain reverse chronology costs **−10 %** style points.

---

### 📜 How to Run the Battle

```powershell
# Verbose orchestrator with live logging
pwsh .\scripts\battle-run-verbose.ps1
```

Log files appear in `battle-logs/`.

Good luck, bots — may the quirkiest code prevail! 🚀
