# TOOLS.md - Tool Notes

## Default: No Tools Required

This bot works with **conversation only** by default. The transformation happens through:
1. Asking the right questions
2. Pushing past sanitized answers
3. Naming patterns
4. Building game structures
5. Holding accountability

All state is stored in Markdown files (`MEMORY.md`, `memory/*.md`).

---

## Optional Integrations

If your Clawdbot has these tools available, Nika can use them:

### TickTick
**What it does:** Sync daily levers as tasks, track completion automatically.

**How to use:**
- After building game structure, ask: "Add my daily levers to TickTick"
- Evening review can check TickTick completion instead of asking

### Obsidian
**What it does:** Store protocol outputs in your Obsidian vault, link with daily notes.

**How to use:**
- Set workspace to an Obsidian vault folder
- Protocol outputs become searchable notes
- Daily logs integrate with Obsidian daily notes

### Calendar (Google/Apple)
**What it does:** Block time for daily levers, schedule protocol run day.

**How to use:**
- After protocol: "Block 2 hours each morning for my daily levers"
- Before protocol: "Block tomorrow 7am-9pm for protocol day"

### Git
**What it does:** Track game structure evolution over time, measure identity shift.

**How to use:**
- Commit game structure changes after each refinement
- Compare versions to see growth
- Keep changelog of protocol iterations

---

## Adding Tools

To enable these integrations:

1. Check if the skill exists in your Clawdbot:
   ```
   ls ~/clawdbot/skills/
   ```

2. Skills are auto-loaded if available. Just ask the bot to use them.

3. For custom integrations, add skill to `~/clawdbot/skills/` and restart gateway.

---

## Keep It Simple

Don't over-engineer. The protocol works without any tools.

Tools are for **automation and convenience**, not requirements.

If you find yourself spending more time setting up tools than doing the actual work, stop. Just use the bot for conversation and track things manually.
