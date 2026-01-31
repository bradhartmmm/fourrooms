# /absorb

Grab content from anywhere and save it locally for processing.

**Arguments:** `$ARGUMENTS`

---

## What This Does

Takes a URL, file, or source and extracts the content into a local file.

**Input:** URL, file path, or pasted content
**Output:** Clean text file in `transcripts/`

---

## Quick Start

```
/absorb https://www.youtube.com/watch?v=abc123
/absorb https://vimeo.com/123456789
/absorb https://example.com/blog-post
/absorb path/to/document.pdf
/absorb recording.mp3
```

---

## Supported Sources

| Source | How It Works |
|--------|--------------|
| **YouTube** | Downloads captions via yt-dlp |
| **Vimeo** | Gets transcript via API (needs key for private) |
| **Web pages** | Extracts main content, strips nav/ads |
| **PDF** | Extracts text content |
| **Audio/Video files** | Transcribes via Whisper |
| **Local text files** | Copies to transcripts folder |
| **Pasted text** | Saves directly |

---

## How To Use

### Step 1: Identify Source Type

Parse the argument:

- **YouTube:** Contains `youtube.com` or `youtu.be`
- **Vimeo:** Contains `vimeo.com`
- **Web page:** Starts with `http://` or `https://`
- **PDF:** Ends with `.pdf`
- **Audio:** Ends with `.mp3`, `.m4a`, `.wav`
- **Video:** Ends with `.mp4`, `.mov`, `.webm`
- **Local file:** Path exists on disk
- **Pasted text:** None of the above, treat as raw content

### Step 2: Extract Content

**YouTube:**
```bash
# Check for yt-dlp
which yt-dlp || echo "Install with: brew install yt-dlp"

# Download transcript (VTT format - no ffmpeg needed)
yt-dlp --write-auto-sub --sub-lang en --skip-download -o "transcripts/%(title)s" "URL"

# Convert VTT to plain text using Python (no ffmpeg required)
python3 -c "
import re
import sys

with open('INPUT.vtt', 'r') as f:
    content = f.read()

lines = content.split('\n')
text_lines = []
for line in lines:
    # Skip VTT headers, timestamps, position markers
    if line.startswith('WEBVTT') or line.startswith('Kind:') or line.startswith('Language:'):
        continue
    if re.match(r'^\d+$', line.strip()):
        continue
    if re.match(r'^\d{2}:\d{2}:', line):
        continue
    if 'align:start position:' in line:
        continue
    if not line.strip():
        continue
    # Remove HTML tags like <c> </c>
    clean = re.sub(r'<[^>]+>', '', line)
    if clean.strip():
        text_lines.append(clean.strip())

# Remove consecutive duplicate lines (VTT repeats lines)
final = []
prev = ''
for line in text_lines:
    if line != prev:
        final.append(line)
        prev = line

print('\n'.join(final))
" > OUTPUT.txt
```

**Note:** VTT files work without ffmpeg. The Python script handles conversion directly.

**Vimeo:**
```bash
# Get video info via Vimeo API
# Check for text tracks
# Download and convert VTT to plain text
```

**Web pages:**
```bash
# Fetch page
curl -s "URL" > temp.html

# Extract main content (use readability algorithm or simple extraction)
# Strip scripts, styles, navigation
# Convert to plain text
```

**PDF:**
```bash
# Check for pdftotext
which pdftotext || echo "Install with: brew install poppler"

# Extract text
pdftotext "file.pdf" "transcripts/filename.txt"
```

**Audio/Video (local files):**
```bash
# Check for whisper
which whisper || echo "Install with: pip install openai-whisper"

# Transcribe
whisper "file.mp3" --output_dir transcripts/ --output_format txt
```

**Pasted text:**
```bash
# Save directly to transcripts/
# Ask user for a filename
```

### Step 3: Clean the Content

- Remove timestamps (optional - ask user)
- Strip HTML artifacts
- Normalize whitespace
- Keep paragraph breaks

### Step 4: Save and Report

Save to `transcripts/` with a clean filename (slugified title).

```
✅ Content absorbed!

📄 Saved to: transcripts/how-to-build-a-funnel.txt
📊 Length: 4,523 words
🎬 Source: YouTube

Next steps:
  /extract-workflow transcripts/how-to-build-a-funnel.txt
  /gamma transcripts/how-to-build-a-funnel.txt
```

---

## Prerequisites

Different sources need different tools:

| Source | Required | Install |
|--------|----------|---------|
| YouTube | yt-dlp + Python 3 | `brew install yt-dlp` (Python is pre-installed on Mac) |
| Vimeo | Vimeo API key | Add to `.env` |
| PDF | poppler | `brew install poppler` |
| Audio | whisper | `pip install openai-whisper` |
| Web | curl | Built-in |

**Note:** ffmpeg is NOT required for YouTube transcripts. The VTT-to-text conversion uses Python.

---

## Notes

- YouTube auto-captions may have errors
- Whisper transcription can take a few minutes for long audio
- Web extraction works best on article/blog content
- Large files are saved as-is; summarize after if needed
