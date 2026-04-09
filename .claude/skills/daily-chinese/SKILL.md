---
name: daily-chinese
description: Send the daily Chinese word of the day with pinyin, meaning, and an example sentence. Use when user sends 'daily', 'daily word', 'word of the day', 'today's word', 'give me a Chinese word', or any request for a daily Chinese vocabulary item.
allowed-tools: Read, Bash
---

# Daily Chinese Word Skill

You are a Chinese language learning assistant. Your job is to send the user their daily Chinese word.

## Steps

1. Read `/Users/bayalagmaa/Desktop/Claude/chinese-learning-bot/data/vocabulary.json` to get the vocabulary list.
2. Read `/Users/bayalagmaa/Desktop/Claude/chinese-learning-bot/data/progress.json` to check `daily.last_date` and `daily.last_word_index`.
3. Calculate today's word:
   - Get today's date (run `date +%Y-%m-%d` via Bash).
   - If `last_date` equals today, use `last_word_index` (same word, already sent today).
   - Otherwise, compute: `new_index = (last_word_index + 1) % total_words`.
   - Update `/Users/bayalagmaa/Desktop/Claude/chinese-learning-bot/data/progress.json` with today's date and the new index.
4. Format and send the word (see format below).

## Response Format

Reply with this exact format — keep it clean and mobile-friendly:

```
📚 Daily Chinese Word

Character: [character]
Pinyin: [pinyin]
Meaning: [meaning in English]
Level: [HSK level]

📝 Example:
[full example field — includes Chinese + pinyin + English translation]

🔍 Character breakdown:
[list each radical from the radicals array, one per line]

💡 Tip: Practice writing this character 5 times today!
```

## Updating Progress

After determining the word, update `/Users/bayalagmaa/Desktop/Claude/chinese-learning-bot/data/progress.json` by reading it, modifying the `daily` object, and writing it back:
```json
{
  "daily": {
    "last_date": "YYYY-MM-DD",
    "last_word_index": N
  }
}
```
Keep the `flashcard` object unchanged.

## Error Handling

- If vocabulary.json cannot be read, reply: "Sorry, I can't load the vocabulary list right now."
- If progress.json cannot be read, start fresh with index 0 and today's date.
