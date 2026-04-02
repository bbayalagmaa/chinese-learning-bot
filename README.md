# Chinese Learning Bot

A Telegram bot that helps you learn Mandarin Chinese — built with Claude Channels (Path A) for AUM AI Class Project 2.

**Platform:** Telegram  
**Architecture:** Claude Code + Claude Channels + custom skills  
**Bot:** Connect via Telegram (see setup below)

---

## What It Does

The bot has 4 skills covering all aspects of Chinese vocabulary learning:

| Skill | Trigger | What It Does |
|-------|---------|--------------|
| `daily-chinese` | "daily word", "word of the day" | Sends one new HSK word per day with pinyin, meaning, and example sentence |
| `chinese-flashcard` | "quiz me", "flashcard", "test me" | Interactive vocab quiz — guess the meaning, get feedback + score |
| `chinese-translate` | Send any Chinese text | Translates + explains pinyin, grammar, and character components |
| `chinese-practice` | "stroke order for 好", "how to write 中" | Step-by-step stroke order, radical breakdown, and mnemonics |

---

## Example Conversations

### Daily Word
```
You: daily word
Bot: 📚 Daily Chinese Word
     Character: 梦想
     Pinyin: mèng xiǎng
     Meaning: dream / aspiration
     Level: HSK4
     ...
```

### Flashcard Quiz
```
You: quiz me
Bot: 🃏 Flashcard Quiz! What does this mean?
       学习 (xué xí)
     Type your answer 👇

You: to study
Bot: ✅ Correct! Your score: 3/4 this session
```

### Translate
```
You: 我爱学习汉语
Bot: 🗣 Sentence: 我爱学习汉语
     Translation: I love studying Chinese
     ...
```

### Writing Practice
```
You: stroke order for 好
Bot: ✍️ Writing Practice: 好
     Strokes: 6 total
     1. Left-falling stroke (woman 女 component)...
     💡 好 = woman (女) + child (子) = "good/beautiful" ❤️
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

Send these messages to your bot in Telegram:
- `daily word` → should get today's Chinese word
- `quiz me` → should start a flashcard session
- `你好` → should translate it
- `stroke order for 好` → should give writing instructions

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

- **4 GitHub issues** — one per skill (#1, #2, #3, #4)
- **4 feature branches** — `feature/daily-chinese`, `feature/chinese-flashcard`, `feature/chinese-translate`, `feature/chinese-practice`
- **2 git worktrees** — `chinese-flashcard` and `chinese-translate` developed in parallel:
  ```bash
  git worktree add ../chinese-bot-flashcard feature/chinese-flashcard
  git worktree add ../chinese-bot-translate feature/chinese-translate
  ```
- **4 PRs merged** — #5, #6, #7, #8

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
