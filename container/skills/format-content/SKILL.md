---
name: format-content
description: Format raw text into clean structure (bullets, headers, tables, numbered lists) for different platforms like email, Telegram, docs, or Slack.
---

# Format Content

Transform content between formats while preserving meaning. Handles structural changes like bullets to prose, text to tables, and platform-specific formatting.

## When to Use

- "Convert this to bullets"
- "Make this a table"
- "Turn this into paragraphs"
- "Format this for Telegram/email/Slack"
- "Restructure this"
- "Put this in a table"
- "Clean up this formatting"

## Process

### 1. Identify Source and Target

| From | To | Use When |
|------|-----|----------|
| Prose | Bullets | Dense text needs to be skimmable |
| Bullets | Prose | Need polished, readable output |
| Text | Table | Comparing items, structured data |
| Table | Text | Need to explain, not just show |
| Raw notes | Clean structure | Messy input needs organizing |
| Any | Platform-specific | Targeting email, Telegram, Slack, docs |

### 2. Apply Transformation

**Prose to bullets:**
- One idea per bullet
- Start each with action verb or key noun
- Parallel structure across bullets
- 7-10 words per bullet max

**Bullets to prose:**
- Group related points
- Add transitions between ideas
- Vary sentence structure
- Maintain logical flow

**Text to table:**
- Identify column headers (attributes)
- Identify rows (items being compared)
- Keep cells concise (phrases, not sentences)
- Use markdown table format

**Raw notes to clean structure:**
- Group related items under headers
- Add hierarchy where natural
- Remove duplicates
- Order logically (chronological, priority, or thematic)

### 3. Platform-Specific Formatting

**Email:**
- Short paragraphs, lots of white space
- Bold for key info sparingly
- No complex markdown (most email clients strip it)
- Clear action items at the end

**Telegram:**
- Keep messages short (under 4096 chars)
- Use bold (*text*) and italic (_text_) sparingly
- Break long content into multiple messages
- No markdown tables (they don't render)

**Slack:**
- Use Slack markdown (bold, bullets, code blocks)
- Keep messages scannable
- Use thread-friendly lengths
- Emoji sparingly for visual anchors

**Docs/README:**
- Full markdown with headers, tables, code blocks
- Table of contents for long docs
- Consistent header hierarchy

### 4. Present Result

Show the formatted content. Offer to adjust format or platform targeting.

## Anti-Patterns

- Don't change meaning while changing format
- Don't create single-item bullet lists (keep as prose)
- Don't make tables with only one column (use a list)
- Don't lose nuance when condensing
- Don't add filler when expanding
- Don't over-format. Sometimes plain text is best
