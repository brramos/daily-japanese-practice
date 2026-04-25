---
name: setup
description: >
  This skill sets up the daily Japanese practice schedule and optional iMessage
  delivery. Use when the user says "set up Japanese practice", "configure daily
  Japanese", "start Japanese schedule", or upon first install of the plugin.
metadata:
  version: "0.1.0"
---

# Setup Daily Japanese Practice

Guide the user through configuring their daily Japanese sentence schedule and optional iMessage delivery.

## Step 1: Ask Preferences

Use AskUserQuestion to gather:

1. **Delivery time** — What time should the daily sentence arrive? Offer morning (8am), afternoon (12pm), evening (6pm), or let them specify a custom time.

2. **iMessage delivery** — Ask if they want the sentence sent via iMessage in addition to the Cowork notification. If yes, ask for the recipient phone number or Apple ID email.

## Step 2: Save iMessage Config

If the user opted into iMessage delivery, create the config file:

```bash
mkdir -p ~/.config/daily-japanese-practice
```

Then write `~/.config/daily-japanese-practice/config.json` with:

```json
{
  "imessage_recipient": "<phone_number_or_email>",
  "setup_date": "<today's ISO date>"
}
```

The `setup_date` is used by the daily-sentence skill to calculate the difficulty progression month.

## Step 3: Create the Scheduled Task

Use the `create_scheduled_task` tool with these parameters:

- **taskId**: `daily-japanese-sentence`
- **description**: `Daily Japanese sentence translation challenge`
- **cronExpression**: Based on the user's chosen time (e.g., `0 8 * * *` for 8am)
- **prompt**: `Run the daily-sentence skill from the daily-japanese-practice plugin. Follow all instructions in the skill, including checking for iMessage delivery config.`

## Step 4: Confirm

Tell the user setup is complete. Summarize:
- What time the sentence will arrive
- Whether iMessage delivery is enabled (and to which recipient)
- That difficulty starts at 1st grade and progresses monthly
- They can say "Give me a Japanese sentence" any time for an extra practice round
