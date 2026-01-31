# FR-Workflows

**Turn any content into a reusable workflow. Zero coding required.**

Built for Four Rooms. Get from zero to magic in 5 minutes.

---

## The "Holy Shit" Moment

Once you're set up, try this:

```
/gamma "5 ways AI is changing small business operations"
```

One command. 30 seconds. Live presentation URL.

**Demo key included** - go nuts, we have lots of credits.

---

## 5-Minute Setup

### 1. Get Claude Pro or Max

Go to **https://claude.ai** and sign up for:
- **Claude Pro** ($20/mo) - Great for getting started
- **Claude Max** ($100/mo) - Unlimited usage

### 2. Download Claude Desktop

Download from **https://claude.ai/download**

Install it like any other app.

### 3. Download This Repo

**Option A: Download ZIP**
1. Click the green "Code" button on GitHub
2. Click "Download ZIP"
3. Unzip it to your Desktop (or wherever you want)

**Option B: Clone with GitHub Desktop**
1. Download GitHub Desktop from https://desktop.github.com
2. Click "Clone a repository"
3. Paste the repo URL

### 4. Open in Claude Desktop

1. Open Claude Desktop
2. Click "Choose Project" (or drag the FR-Workflows folder in)
3. Select the FR-Workflows folder you downloaded

### 5. Try the Magic

Type this in Claude:

```
/gamma "How to automate your business with AI"
```

Watch the magic happen. You'll get a live presentation URL in ~30 seconds.

---

## What You Can Do

| Skill | What It Does | Example |
|-------|--------------|---------|
| `/gamma` | Instant presentations | `/gamma "Your topic"` |
| `/absorb` | Grab content from anywhere | `/absorb https://youtube.com/...` |
| `/extract-workflow` | Turn content into workflow | `/extract-workflow transcripts/file.txt` |
| `/workflow` | Build workflows interactively | `/workflow start` |
| `/tiktok` | TikTok/Reels content strategy | `/tiktok brainstorm` |

---

## The Pipeline

```
Content → Absorb → Extract → Present
   ↓        ↓        ↓         ↓
YouTube  /absorb  /extract   /gamma
Article  saves    creates    makes
PDF      locally  workflow   slides
```

**Example flow:**
```
/absorb https://youtube.com/watch?v=abc123
/extract-workflow transcripts/the-video.txt
/gamma completed-workflows/the-video.prompt.md
```

---

## Cool Stuff People Built

Using `/gamma` with workflows:

- [Start with Why - Simon Sinek](https://gamma.app/docs/98emc8mqobfepdd)
- [Principles for Dealing with the Changing World Order - Ray Dalio](https://gamma.app/docs/Principles-for-Dealing-with-the-Changing-World-Order-04uri820a8t00ad?mode=doc)
- [Healing People Pleasing with EFT Tapping](https://gamma.app/docs/Healing-People-Pleasing-with-EFT-Tapping-bsg1a6r4avdv4s0?mode=doc)
- [3 Time-Friendly Workouts for Busy Parents Over 50](https://gamma.app/docs/3-Time-Friendly-Workouts-for-Busy-Parents-Over-50-3nlhztrat1pxvft?mode=doc)
- [The Football Folk - 5 Ways to Improve](https://gamma.app/docs/The-Football-Folk-4d26r9wh9whm643?mode=doc)

---

## Folder Structure

```
FR-Workflows/
├── .claude/commands/      # Skills (the magic)
│   ├── absorb.md
│   ├── extract-workflow.md
│   ├── gamma.md
│   ├── tiktok.md
│   └── workflow.md
├── completed-workflows/   # Your extracted workflows
├── transcripts/           # Absorbed content
├── templates/             # Workflow templates
├── examples/              # Example workflows
└── .env                   # API keys (included!)
```

---

## API Keys

The `.env` file is already included with a demo Gamma key:

```
GAMMA_API_KEY=sk-gamma-6VFufds97bR7JWyLpM9PvRfwD0OmZpkQRZrDKCDY
```

Lots of credits. Go wild.

---

## FAQ

**Do I need to code?**
No. Claude handles everything.

**Do I need to use the terminal?**
No. Everything works through Claude Desktop's chat interface.

**What if something breaks?**
Ask Claude. Copy the error, paste it, ask "what does this mean?"

**Can I create my own skills?**
Yes. Skills are just markdown files. Ask Claude to help you make one.

**What's the difference between a skill and a workflow?**
- **Skill** = A command that does something (like `/gamma`)
- **Workflow** = A structured process extracted from content

---

## Need Help?

Just ask Claude:
- "I'm stuck, help me"
- "What else can I automate?"
- "Walk me through creating a workflow"

---

*Built for Four Rooms. Turn knowledge into action.*
