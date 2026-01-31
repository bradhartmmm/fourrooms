# /extract-workflow

Extract an actionable workflow from content (transcript, article, notes).

**Arguments:** `$ARGUMENTS`

---

## What This Does

Analyzes content and extracts a structured, reusable workflow.

**Input:** Path to transcript or content file
**Output:** Workflow files in `completed-workflows/`

---

## Usage

```
/extract-workflow transcripts/my-video.txt
/extract-workflow path/to/notes.md
```

Or paste content directly after the command.

---

## What It Creates

For each workflow, three files are generated:

1. **`{slug}.workflow.json`** - Structured data (steps, inputs, tools)
2. **`{slug}.prompt.md`** - Human-readable guide with instructions
3. **`{slug}.meta.json`** - Source info and timestamps

---

## Process

### Step 1: Read the Content

Load the transcript or content file. If pasted directly, use that.

### Step 2: Extract the Workflow

Analyze for:
- **Outcome:** What does the user achieve?
- **Inputs:** What info do they need before starting?
- **Steps:** The actual process, in order
- **Tools:** What software/services are mentioned?

Structure as JSON:
```json
{
  "title": "Short descriptive title",
  "source": "Where this came from",
  "outcome": "What the user achieves",
  "inputs": [
    {"name": "target_audience", "description": "Who is this for?", "required": true}
  ],
  "capabilities_needed": [
    {
      "capability": "send_emails",
      "description": "Send automated emails",
      "common_tools": ["Gmail", "Mailchimp", "ConvertKit"],
      "minimum_viable": "Gmail"
    }
  ],
  "steps": [
    {
      "step_number": 1,
      "action": "What to do",
      "details": "Specific instructions",
      "output": "What this step produces"
    }
  ],
  "estimated_time": "2-4 hours",
  "automation_potential": "high"
}
```

**Key principle:** Describe CAPABILITIES, not specific tools. Always include a minimum viable option.

### Step 3: Generate the Prompt File

Create a human-readable guide:

```markdown
# [Workflow Title]

[One sentence describing what this achieves]

## What You'll Need

Before starting, have these ready:
- **[Input 1]**: [description]
- **[Input 2]**: [description]

## Tools/Services

This workflow uses:
- **[Capability]** - [common tools that work]

## The Process

[Full explanation of the methodology]

## Steps

1. [First step with details]
2. [Second step with details]
...

---
*Source: [Where this came from]*
```

### Step 4: Save to completed-workflows/

Create a slug from the title (lowercase, hyphens):
- `completed-workflows/{slug}.workflow.json`
- `completed-workflows/{slug}.prompt.md`
- `completed-workflows/{slug}.meta.json`

### Step 5: Report

```
✅ Workflow extracted!

📋 Title: [title]
📁 Saved to: completed-workflows/{slug}/

Files created:
  - {slug}.workflow.json
  - {slug}.prompt.md
  - {slug}.meta.json

Next steps:
  /gamma completed-workflows/{slug}.prompt.md
```

---

## Tips

- Focus on actionable steps, skip intros/outros/tangents
- If content doesn't have a clear workflow, say so
- Be tool-agnostic when possible (list alternatives)
- Include enough detail that someone could follow without watching the source
- The prompt.md should be self-contained and useful on its own

---

## Notes

- Works best with tutorial/how-to content
- Short, focused content (under 20 min) extracts better
- If source mentions specific tools, note them but also suggest alternatives
