# Clawdbot Setup Guide

How to install the Transformation Protocol Bot into Clawdbot.

---

## Easy Setup (Recommended)

**1. Clone the repo:**
```bash
git clone https://github.com/YOUR_USERNAME/Nika.git
cd Nika
```

**2. Choose a bot name (optional):**
Default is `Nika`. If you want a different name, use it in place of `Nika` below. Also choose a short
account id for bindings (shown as `BOT_ACCOUNT_ID`, examples: `protocol`, `nika`, `coach`).

**3. Ask your Clawdbot to set it up:**
> "Set up a new agent called 'Nika' using the workspace at ~/Nika"

Clawdbot will:
- Create the Telegram bot (guides you through @BotFather)
- Update `clawdbot.json` with agent config
- Add bindings for the new bot
- Restart the gateway

**That's it.** Your bot is ready.

After running the protocol, set up daily reminders (see below).

---

## Manual Setup

If you prefer to configure manually, follow these steps.

### Prerequisites

- Clawdbot installed and running
- Telegram account (for bot creation)
- Access to `~/.clawdbot/clawdbot.json`

---

### Step 1: Create Telegram Bot

1. Open Telegram, find **@BotFather**
2. Send `/newbot`
3. Choose name: `Nika` (or your custom name)
4. Choose username: e.g., `bot_name_protocol`
5. **Save the API token** (looks like `1234567890:ABCdef...`)

---

## Step 2: Create Workspace

```bash
# Create workspace directory
mkdir -p ~/clawd-nika

# Copy all files from this repo
cp -r /path/to/Nika/* ~/clawd-nika/
```

Your workspace should look like:
```
~/clawd-nika/
├── SOUL.md
├── AGENTS.md
├── IDENTITY.md
├── TOOLS.md
├── MEMORY.md
├── USER.md
├── HEARTBEAT.md
├── SETUP.md
├── memory/
│   ├── game-structure.md
│   └── daily-template.md
└── references/
    ├── PROTOCOL.md
    ├── onboarding.md
    ├── morning.md
    ├── interrupts.md
    ├── evening.md
    ├── check-ins.md
    └── game-template.md
```

---

## Step 3: Configure Clawdbot

Edit `~/.clawdbot/clawdbot.json`:

### Add Agent to `agents.list`:
```json
{
  "agents": {
    "list": [
      // ... existing agents ...
      {
        "id": "nika",
        "identity": {
          "name": "Nika",
          "theme": "coach",
          "emoji": "☀️"
        },
        "workspace": "/home/YOUR_USER/clawd-nika",
        "model": {
          "primary": "anthropic/claude-sonnet-4-5"
        }
      }
    ]
  }
}
```

### Add Telegram Account to `channels.telegram.accounts`:
```json
{
  "channels": {
    "telegram": {
      "accounts": {
        // ... existing accounts ...
        "BOT_ACCOUNT_ID": {
          "botToken": "YOUR_BOT_TOKEN_FROM_BOTFATHER"
        }
      }
    }
  }
}
```

### Add Binding to `bindings`:
```json
{
  "bindings": [
    // ... existing bindings ...
    {
      "agentId": "nika",
      "match": {
        "channel": "telegram",
        "accountId": "BOT_ACCOUNT_ID"
      }
    }
  ]
}
```

---

## Step 4: Restart Gateway

Use the gateway tool to restart:
```
/restart
```

Or ask the bot to restart the gateway.

---

## Step 5: Test

Send a message to your new bot on Telegram:
> "I want to run the transformation protocol"

---

## Protocol Files

All protocol content is **already included** in this folder:
- `references/` — Theory + step-by-step guides (morning/interrupts/evening)
- `memory/` — Game structure + daily log template

No additional setup needed.

---

## Setting Up Daily Reminders

After protocol is complete, set up daily accountability reminders:

**Option 1: Ask the bot**
> "Set up daily reminders: 8am for morning levers, 1pm for progress check, 9pm for evening review"

**Option 2: CLI**
```bash
clawdbot cron add --name "Morning Lever" --cron "0 8 * * *" --tz "YOUR_TIMEZONE" \
  --session isolated --agent nika --deliver --channel telegram \
  --message "☀️ Morning. What daily levers are you starting with?"

clawdbot cron add --name "Midday Check" --cron "0 13 * * *" --tz "YOUR_TIMEZONE" \
  --session isolated --agent nika --deliver --channel telegram \
  --message "☀️ Midday. Moving toward life you want or life you hate?"

clawdbot cron add --name "Evening Review" --cron "0 21 * * *" --tz "YOUR_TIMEZONE" \
  --session isolated --agent nika --deliver --channel telegram \
  --message "☀️ Evening review. Did you complete your levers? What did you avoid?"
```

---

## Example Full Config Snippet

```json
{
  "agents": {
    "list": [
      {
        "id": "nika",
        "identity": {
          "name": "Nika",
          "theme": "coach",
          "emoji": "☀️"
        },
        "workspace": "/home/YOUR_USER/clawd-nika",
        "model": {
          "primary": "anthropic/claude-sonnet-4-5"
        }
      }
    ]
  },
  "bindings": [
    {
      "agentId": "nika",
      "match": {
        "channel": "telegram",
        "accountId": "BOT_ACCOUNT_ID"
      }
    }
  ],
  "channels": {
    "telegram": {
      "accounts": {
        "BOT_ACCOUNT_ID": {
          "botToken": "YOUR_BOT_TOKEN"
        }
      }
    }
  }
}
```

---

## Troubleshooting

### Bot not responding
- Check gateway is running
- Verify botToken is correct in config
- Check bindings connect the right agent to the right account

### Files not found
- Verify workspace path in config matches actual location
- Check file permissions

### Reminders not firing
- Verify cron is enabled in config
- Check cron jobs exist
