---
name: daily-sentence
description: >
  This skill delivers a daily Japanese sentence translation challenge. Use when
  the user says "Japanese sentence", "daily Japanese", "translation practice",
  "give me a sentence to translate", or "nihongo practice". Also triggered
  automatically by the scheduled task.
metadata:
  version: "0.2.0"
---

# Daily Japanese Sentence

Present the user with one Japanese sentence to translate. The difficulty progresses monthly based on Japanese elementary school grade levels.

## Determine Difficulty Level

Calculate the current level from today's date. The starting month is the month the user first installed this plugin (default: the current month if unknown). Each subsequent month advances one grade level, capping at Grade 6.

| Months since start | Level                  | Description                                                                                                  |
| ------------------ | ---------------------- | ------------------------------------------------------------------------------------------------------------ |
| 0                  | 1st grade (小学1年生)  | Simple Subject+Verb or Subject+Object+Verb. Basic hiragana, katakana, Grade 1 kanji (一, 二, 大, 小, 日, 月, 山, 川). 3-7 words. |
| 1                  | 2nd grade (小学2年生)  | Slightly longer sentences. Grade 1-2 kanji. Basic particles (は, が, を, に, で). Present tense ます form.      |
| 2                  | 3rd grade (小学3年生)  | Past tense, て-form, い/な adjectives, Grade 1-3 kanji, compound sentences.                                   |
| 3                  | 4th grade (小学4年生)  | Relative clauses, たい form, から/ので, Grade 1-4 kanji.                                                       |
| 4                  | 5th grade (小学5年生)  | Conditional forms (たら, ば), passive voice basics, 2-3 sentence passages.                                     |
| 5+                 | 6th grade (小学6年生)  | Honorifics intro, complex structures, short paragraphs. Stay here but vary topics and grammar.                |

## Vocabulary Personalization (Optional)

Before generating the sentence, attempt to read the user's vocabulary notes to personalize the sentence. Try the following sources in order — use whichever one exists, or skip this step entirely if none are found:

1. **Logseq** — Use the Logseq MCP tools if available: look for pages named "Known Japanese Words" and "kanji" in the user's graph.
2. **Obsidian** — Use the filesystem MCP tools if available: look for files like `Known Japanese Words.md` or `kanji.md` in the user's vault.
3. **Local files** — Check the user's Documents folder for any files matching those names.

If vocabulary data is found, incorporate some known words into the sentence so the user gets reinforcement, while also introducing 1-2 new words or grammar points appropriate to the current level.

If no vocabulary source is found, simply generate an appropriate sentence for the level. Do not ask the user to set anything up — just proceed.

## What to Present

1. A short greeting in Japanese — vary it daily. Use おはよう, こんにちは, today's date in Japanese, a seasonal reference, a weather comment, etc.

2. The sentence in Japanese with furigana in parentheses after each kanji compound. Example:
   > 山(やま)に 行(い)きます。

3. A hint — one short contextual clue or grammar note to assist (e.g., "Remember: に marks the destination").

4. The current level label (e.g., "Level: 小学2年生").

5. Do NOT reveal the English translation. Tell the user to try translating it and that you will check their answer if they reply.

## Sentence Guidelines

- Use natural, everyday Japanese — things a child at that grade level would actually say or read.
- Vary topics daily: school, family, animals, food, weather, hobbies, daily routines, seasons, travel.
- Never repeat sentences across runs. Vary vocabulary and grammar patterns each day.
- Each sentence should reinforce at least one grammar point appropriate to the current level.

## iMessage Delivery

After generating the sentence, check if a file exists at `~/.config/daily-japanese-practice/config.json`. If it does, read it and look for an `imessage_recipient` field.

If a recipient is configured, use the iMessage MCP tool (`send_imessage`) to send the sentence to that recipient. Format the iMessage as a clean, readable text message:

```
おはよう！🇯🇵

今日の文 (Today's sentence):
山(やま)に 行(い)きます。

💡 Hint: に marks the destination

Level: 小学1年生

Try translating and reply with your answer!
```

If no config file exists or no recipient is set, skip iMessage delivery and just present the sentence in the Cowork notification as usual.

## Tone

Encouraging and brief. This is a quick daily challenge, not a full lesson. Keep the total message concise — greeting, sentence, hint, level, and a short encouragement to try translating.
