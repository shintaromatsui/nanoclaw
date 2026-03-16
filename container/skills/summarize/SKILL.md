---
name: summarize
description: Summarize long text, articles, conversations, or documents into concise key points. Supports multiple output formats.
---

# Summarize

Distill long-form content into concise, scannable summaries that capture the essential information.

## When to Use

- "Summarize this..."
- "Give me the key points"
- "TLDR"
- "What's the main takeaway?"
- "Condense this"
- "Sum this up"

## Process

### 1. Get Content

Sources:
- Direct text paste
- Forwarded message or conversation
- Referenced document or article

### 2. Identify Content Type

| Type | Focus On |
|------|----------|
| Article | Main argument, key evidence, conclusion |
| Meeting/conversation | Decisions, action items, owners |
| Research | Findings, methodology, implications |
| Email thread | Key asks, decisions, next steps |
| Document | Purpose, main sections, recommendations |

### 3. Generate Summary

Pick the right format based on content and request.

**Quick TLDR (default):**
```
TLDR: [2-3 sentences max]
```

**Bullet summary:**
```
Key points:
- [Point 1]
- [Point 2]
- [Point 3]
```

**Executive summary:**
```
[Problem/context in 1-2 sentences]

[Key findings/recommendations in 2-3 sentences]

[Next steps or implications in 1 sentence]
```

**Meeting summary:**
```
Decisions:
- [What was decided]

Action items:
- [Task] -- [Owner]

Open questions:
- [Unresolved items]
```

### 4. Adjust for Context

If unclear, ask:
- How detailed? (bullet points vs paragraph)
- What is the use case? (sharing with others, personal reference, decision-making)

## Length Guidelines

| Original Length | Summary Target |
|-----------------|----------------|
| 1 page | 3-5 bullet points |
| 5 pages | 1 paragraph + bullets |
| 10+ pages | Executive summary format |
| Conversation | Decisions + action items |

## Anti-Patterns

- Don't pad with filler words. Every word should add value
- Don't include context the reader already knows
- Don't lose important nuance in oversimplification
- Don't just excerpt. Synthesize
- Don't miss action items in meeting summaries
