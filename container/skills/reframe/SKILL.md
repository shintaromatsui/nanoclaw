---
name: reframe
description: Present 3-5 alternative framings of a stuck problem to unlock new approaches. Use when someone says "reframe this", "I'm stuck on", "how else could I think about", "flip this", "different angle", "I keep going in circles", "new perspective", "think about this differently", or needs to break out of a mental rut.
---

# Problem Reframing

When you're stuck, the problem isn't usually that you lack information — it's that you're looking at it wrong. This skill generates 3-5 genuinely different ways to frame the same problem, each opening up different solutions.

## Input

Parse the message to extract:
- **Problem or situation** (required): What you're stuck on
- **Current framing** (optional): How you're currently thinking about it
- **Constraint** (optional): What feels immovable ("I can't change X", "budget is fixed")

Examples:
- "reframe: we can't hire fast enough to hit our roadmap"
- "I keep putting off the hard conversation with my manager — reframe this"
- "help me think differently about choosing between these two job offers"

## Process

### Step 1: Surface the Current Frame

Before generating alternatives, make the current framing explicit.

- **Current frame:** How is the user thinking about this right now?
- **Implicit assumptions:** What are they taking as fixed that might not be?
- **Hidden "should":** What unspoken rule or expectation is constraining their thinking?

Example:
> "We can't hire fast enough" assumes:
> - Hiring is the only way to add capacity
> - The roadmap is fixed
> - Current team can't be redeployed

### Step 2: Generate Alternative Frames

Produce 3-5 genuinely different framings. Each frame should:
- Change what the "real problem" is
- Suggest different solutions than the current frame
- Challenge at least one assumption from Step 1

**Reframing techniques:**

1. **Flip the constraint:** What if the thing you're treating as fixed is actually the variable?
   - "We can't hire fast enough" → "Our roadmap is too big for our team"

2. **Change the time horizon:** What if this isn't a now problem?
   - "I need to decide between two offers" → "What creates the best options 3 years from now?"

3. **Change the actor:** What if this isn't your problem to solve?
   - "I can't get buy-in from the VP" → "The VP doesn't have the information to say yes"

4. **Invert the goal:** What if the opposite is true?
   - "We need more customers" → "We need fewer, better customers"

5. **Remove the problem:** What if you didn't solve it at all?
   - "How do we reduce churn?" → "What if churn is healthy and we just need faster acquisition?"

6. **Zoom in / Zoom out:** Change the altitude
   - Zoom in: "Which specific user segment is actually churning?"
   - Zoom out: "Is retention even the right metric for this stage?"

7. **Ask who benefits:** Follow the incentives
   - "Why won't the team adopt this tool?" → "Who benefits from the current way of doing things?"

### Step 3: For Each Frame, Show the Path

For each reframe:
- **Frame:** The reframed problem statement
- **What changes:** New focus under this frame
- **First move:** What you'd do first
- **What you'd stop doing:** What becomes irrelevant

## Output Format

```
# Reframe: [Original Problem]

## Current Frame
**You're seeing this as:** [current framing]
**Hidden assumptions:** [what's being taken as fixed]

## Alternative Frames

### Frame 1: [Name — 3-5 words]
**Reframed problem:** [new problem statement]
**Technique:** [which reframing technique]
**What changes:** [new focus]
**First move:** [what you'd do]
**You'd stop:** [what becomes irrelevant]

### Frame 2: [Name]
[Same structure]

### Frame 3: [Name]
[Same structure]

## My Read
[Which frame(s) seem most promising and why — be opinionated]
```

## Design Principles

- **Name the current frame first.** You can't escape a frame you haven't identified.
- **Each frame must suggest different actions.** If two frames lead to the same solution, they're not really different frames.
- **Challenge the "obvious" constraint.** The thing the user says can't change is often exactly what should change.
- **Be opinionated at the end.** Listing 5 frames with no recommendation is a cop-out. Say which one you'd bet on.
- **Keep it concrete.** "Think about it differently" is useless. "What if you cut the roadmap in half instead of doubling the team?" is useful.
