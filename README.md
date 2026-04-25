# Daily Japanese Practice

A Claude plugin that delivers a daily Japanese sentence translation challenge, progressing from 1st through 6th grade elementary school level over six months.

## What it does

Each day you receive a Japanese sentence with furigana and a grammar hint — delivered as a Cowork notification and optionally via iMessage. You try to translate it, and Claude checks your answer. The difficulty starts simple (basic hiragana and Grade 1 kanji) and increases each month.

## Install

### From GitHub (remote machine)

```bash
claude plugin add --from https://github.com/brramos/daily-japanese-practice
```

Or clone and install locally:

```bash
git clone https://github.com/brramos/daily-japanese-practice.git
claude plugin add ./daily-japanese-practice
```

### From the .plugin file

If you have the `.plugin` file, open it in Claude and follow the install prompt.

## Setup

After installing, say:

> "Set up my daily Japanese practice"

The setup skill will walk you through choosing a delivery time and optionally enabling iMessage delivery. It creates the daily schedule for you automatically.

### iMessage delivery

During setup, you can provide a phone number or Apple ID to receive the daily sentence as an iMessage. This requires the iMessage MCP to be connected in Cowork. The config is saved locally at `~/.config/daily-japanese-practice/config.json`.

## Optional: Vocabulary tracking

The skill can personalize sentences using your vocabulary notes. It automatically checks for:

- **Logseq** — pages named "Known Japanese Words" and "kanji" in your graph
- **Obsidian** — files named `Known Japanese Words.md` and `kanji.md` in your vault

If found, it weaves in words you already know for reinforcement while introducing new ones. No configuration needed — it just works if the files exist.

## Usage

The skill triggers automatically on schedule, or you can say any time:

- "Give me a Japanese sentence to translate"
- "Japanese practice"
- "Daily Japanese"

## Difficulty progression

| Month | Level | What to expect |
|-------|-------|----------------|
| 1 | 1st grade (小学1年生) | Simple sentences, basic hiragana/katakana, Grade 1 kanji |
| 2 | 2nd grade (小学2年生) | Basic particles, ます form verbs, Grade 1-2 kanji |
| 3 | 3rd grade (小学3年生) | Past tense, て-form, adjectives, compound sentences |
| 4 | 4th grade (小学4年生) | Relative clauses, たい form, から/ので |
| 5 | 5th grade (小学5年生) | Conditionals, passive voice, multi-sentence passages |
| 6+ | 6th grade (小学6年生) | Honorifics, complex structures, short paragraphs |
