# /gamma

Create a Gamma presentation from content using the Gamma API.

**Arguments:** `$ARGUMENTS`

---

## What This Does

Takes your content and generates a polished Gamma presentation automatically.

**Input:** File path, topic, or pasted content
**Output:** Live Gamma presentation URL

---

## Quick Start

```
/gamma "How to automate your business with AI"
```

```
/gamma completed-workflows/lead-magnet-creation.workflow.json
```

---

## How To Use

### Step 1: Get the API Key

Read the API key from `.env` file:

```bash
cat .env | grep GAMMA_API_KEY
```

If not set, ask user to add their key to `.env`:
```
GAMMA_API_KEY=sk-gamma-xxxxx
```

Get your key at: https://gamma.app/settings (Pro account required)

### Step 2: Select Theme (RANDOMIZE for Variety!)

**IMPORTANT: Pick a theme at RANDOM from the options below.** Don't always default to the same one or everything looks like peach-colored slop. Variety is key!

**Available themes - PICK ONE AT RANDOM each time:**

| Theme | Vibe | Best For |
|-------|------|----------|
| `borealis` | Dark, cyan/teal | Tech, AI, automation |
| `aurora` | Dark, purple/blue | Creative, innovation |
| `fluo` | Dark, neon green | Systems, processes |
| `electric` | Vibrant, multi-color | Sales, marketing, energy |
| `gamma` | Warm gradient | Leadership, personal dev |
| `atmosphere` | Light, professional | Business, strategy |

**How to choose:**
1. If the topic strongly suggests a vibe (e.g., "AI automation" → dark theme), match it
2. Otherwise, **randomly select** from the list above
3. NEVER default to `atmosphere` every time - mix it up!

**Image style should match the theme:**
- Dark themes → "futuristic, neon accents, dark background, minimal"
- Light themes → "clean professional, warm lighting, minimal"
- Vibrant themes → "dynamic, bold colors, action-oriented"

**Key principle:** Each presentation should feel fresh. Randomize!

### Step 3: Prepare the Content

**If argument is a file path:** Read and extract the key content
**If argument is text:** Use as the topic/prompt
**If no argument:** Ask user what to create

Transform content into a structured outline:
- Title and overview
- 4-8 key sections with bullet points
- Action steps at the end
- Keep it 500-1500 words

### Step 3b: PIP Mode (for video overlay)

**When generating for PIP video output**, add this to your content prompt:

```
IMPORTANT LAYOUT INSTRUCTION: Keep the bottom-right quadrant of each slide
relatively clear of critical text and images. A video avatar will be overlaid
in that area (approximately 25% width, bottom-right corner). Place key content
in the top, left, and center areas of each slide.
```

This ensures the avatar doesn't cover important content when composited.

### Step 4: Call the API

```bash
curl -X POST "https://public-api.gamma.app/v1.0/generations" \
  -H "X-API-KEY: $GAMMA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "inputText": "[YOUR CONTENT HERE]",
    "textMode": "generate",
    "format": "presentation",
    "numCards": 10,
    "themeId": "borealis",
    "imageOptions": {
      "source": "aiGenerated",
      "style": "futuristic technology, neon cyan and teal, dark background"
    },
    "textOptions": {
      "amount": "medium",
      "tone": "empowering, friendly, direct",
      "audience": "business owners"
    },
    "sharingOptions": {
      "externalAccess": "view"
    }
  }'
```

**Response:** `{"generationId": "xxxxx"}`

### Step 5: Poll for Completion

```bash
curl -X GET "https://public-api.gamma.app/v1.0/generations/{generationId}" \
  -H "X-API-KEY: $GAMMA_API_KEY"
```

Poll every 5 seconds until `status` is `completed` or `failed`.

### Step 6: Build the Correct URL

**IMPORTANT:** API-generated presentations go to a separate folder in Gamma. The API returns a short URL that may not work directly. Build the full URL:

**API returns:** `https://gamma.app/docs/abc123xyz`
**Correct format:** `https://gamma.app/docs/[Title-Slug]-abc123xyz?mode=doc`

To build the correct link:
1. Take the ID from the API response (the part after `/docs/`)
2. Slugify the title (lowercase, hyphens for spaces)
3. Combine: `https://gamma.app/docs/{Title-Slug}-{id}?mode=doc`

**Example:**
- Title: "The Optimus Workflow System"
- ID: `n1m9lk1kuo0044r`
- Result: `https://gamma.app/docs/The-Optimus-Workflow-System-n1m9lk1kuo0044r?mode=doc`

### Step 7: Return Result

```
✅ Gamma presentation created!

📊 [Title]
🔗 [Full URL with ?mode=doc]

Cards: [numCards]
Theme: borealis
Credits used: [credits.deducted]
```

---

## Theme Options

**Dark themes (tech/modern):**
- `borealis` - Best match (default)
- `aurora` - Dark with purple/blue
- `fluo` - Dark with neon green

**For other brands:**
- `gamma` - Orange/pink/purple gradient
- `electric` - Vibrant multi-color
- `atmosphere` - Light pink/purple

---

## API Reference

**Base URL:** `https://public-api.gamma.app/v1.0`
**Auth:** Header `X-API-KEY`
**Docs:** https://developers.gamma.app

**Key Parameters:**
- `inputText` - Your content (max 100k tokens)
- `textMode` - `generate` (AI writes), `condense`, or `preserve`
- `format` - `presentation`, `document`, `webpage`, `social`
- `numCards` - 1-60 for Pro accounts
- `themeId` - Theme ID from /themes endpoint

**Rate Limits:** Hundreds of requests per hour included with Pro.

---

## Troubleshooting

**White screen / broken link:** Use the full URL format with title slug and `?mode=doc`

**401 Unauthorized:** Check API key in `.env`

**Generation failed:** Content may be too long or contain unsupported formatting

---

## Notes

- Generation takes 20-40 seconds
- Each presentation costs ~15-70 credits depending on length
- Presentations are public by default (externalAccess: view)
- Edit generated presentations at gamma.app
