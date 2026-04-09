# Chinese Learning Bot

A Telegram bot that helps you learn Mandarin Chinese — built with Claude Channels (Path A) for AUM AI Class Project 2.

**Platform:** Telegram  
**Bot:** [@selflearningsofiachinese_bot](https://t.me/selflearningsofiachinese_bot)  
**Architecture:** Claude Code + Claude Channels + custom skills  

---

## What It Does

The bot has **6 skills** covering all aspects of Chinese learning (HSK 1 & 2 focused):

| Command | What It Does |
|---------|--------------|
| `daily` | Word of the day — character, pinyin, meaning, and example sentence |
| `slang` | Modern Chinese internet slang and Gen Z expressions (内卷, 躺平, yyds...) |
| `story` | Short Chinese reading story with line-by-line pinyin + comprehension question |
| `flashcard` | Quiz question from HSK 1-2 vocab |
| `answer <your answer>` | Check your flashcard or story comprehension answer |
| `translate <Chinese text>` | Translate + explain any Chinese text with character breakdown |
| `practice <character>` | Radical breakdown, stroke order, and mnemonic for a character |
| `score` | View your flashcard quiz progress |

---

## Example Conversations

### Daily Word
```
You:  daily
Bot:  📚 Daily Chinese Word
      Character: 你好
      Pinyin: nǐ hǎo
      Meaning: hello
      Level: HSK1
      ...
```

### Flashcard Quiz
```
You:  flashcard
Bot:  🃏 What does this mean?
        学习 (xué xí)

You:  answer to study
Bot:  ✅ Correct! Your score: 3/4
```

### Translate
```
You:  translate 我爱学习汉语
Bot:  🗣 我爱学习汉语
      Translation: I love studying Chinese
      ...
```

### Writing Practice
```
You:  practice 好
Bot:  ✍️ Writing Practice: 好
      Strokes: 6 total
      💡 好 = woman (女) + child (子) = "good/beautiful" ❤️
```

### Slang
```
You:  slang
Bot:  🔥 Chinese Slang of the Day
      🛌 躺平 (tǎng píng)
      Meaning: "Lying flat" — rejecting hustle culture...
      Example: 我决定躺平了，不想再卷了。
```

### Story Reading
```
You:  story
Bot:  📖 Reading Practice — HSK1 level
      我的一天 (Wǒ de yī tiān) "My Day"
      ━━━━━━━━━━━━━━━━
      我每天早上七点起床。
      Wǒ měitiān zǎoshang qī diǎn qǐchuáng.
      ...
      ❓ What does the person eat for breakfast?

You:  answer bread and eggs
Bot:  ✅ Correct! Great reading!
```

---

## Setup Instructions

### Prerequisites
- Claude Code installed and logged in (`claude.ai` account, not API key)
- Bun installed: `curl -fsSL https://bun.sh/install | bash`
- Telegram account

### Step 1: Create Your Telegram Bot

1. Open Telegram → search for **@BotFather**
2. Send `/newbot`
3. Choose a name (e.g. "Chinese Learning Bot") and username (e.g. `my_chinese_bot`)
4. Copy the token BotFather gives you (looks like `123456:ABC-DEF...`)

### Step 2: Install the Telegram Plugin

In your terminal, open Claude Code and run:
```
/plugin install telegram@claude-plugins-official
/reload-plugins
```

### Step 3: Configure Your Token

Still in Claude Code:
```
/telegram:configure YOUR_TOKEN_HERE
```

### Step 4: Start the Bot

```bash
claude --channels plugin:telegram@claude-plugins-official
```

### Step 5: Pair Your Telegram Account

1. Open Telegram → find your bot → send any message (e.g. "hello")
2. Your bot will reply with a pairing code (e.g. `abc123`)
3. Back in Claude Code, run:
   ```
   /telegram:access pair abc123
   ```
4. Lock access so only you can use it:
   ```
   /telegram:access policy allowlist
   ```

### Step 6: Test

Send these messages to **[@selflearningsofiachinese_bot](https://t.me/selflearningsofiachinese_bot)**:
- `daily` → today's Chinese word
- `flashcard` → start a quiz
- `translate 你好` → translation + explanation
- `practice 好` → stroke order and mnemonic
- `score` → view your quiz progress

> **Important:** Claude Code must be running with `--channels` for the bot to respond. Keep the terminal open during your demo.

---

## Project Structure

```
chinese-learning-bot/
├── .claude/
│   └── skills/
│       ├── daily-chinese/SKILL.md      # Daily word skill
│       ├── chinese-flashcard/SKILL.md  # Quiz skill
│       ├── chinese-translate/SKILL.md  # Translation skill
│       └── chinese-practice/SKILL.md  # Writing practice skill
├── data/
│   ├── vocabulary.json                 # 20-word HSK1-4 dataset
│   └── progress.json                   # Tracks quiz scores & daily word
├── .gitignore
└── README.md
```

---

## Git Workflow Evidence

This project was built using proper git workflow:

- **6 GitHub issues** — one per skill (#1–#4, #9–#10)
- **6 feature branches** — one per skill
- **4 git worktrees** — skills developed in parallel:
  ```bash
  # Round 1
  git worktree add ../chinese-bot-flashcard feature/chinese-flashcard
  git worktree add ../chinese-bot-translate feature/chinese-translate
  # Round 2
  git worktree add ../chinese-bot-slang feature/chinese-slang
  git worktree add ../chinese-bot-story feature/chinese-story
  ```
- **6 PRs merged** — #5, #6, #7, #8, #11, #12

---

## Vocabulary Data

The bot includes 20 HSK words across levels HSK1–HSK4, covering:
- Basic greetings and daily life (HSK1)
- Work, time, emotions (HSK2)
- Travel, health, perseverance (HSK3)
- Dreams and opportunity (HSK4)

Each word includes: character, pinyin, meaning, HSK level, example sentence with translation, and radical breakdowns.

---

## Author

**Sofia (bbayalagmaa)** — AUM Business Administration / Data Science  
GitHub: [bbayalagmaa](https://github.com/bbayalagmaa)
