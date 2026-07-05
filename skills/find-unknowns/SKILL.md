---
name: find-unknowns
description: Behavioral guidelines for finding task unknowns before, during, and after agentic coding work. Use when planning ambiguous tasks, entering unfamiliar codebases or domains, prompting AI agents, prototyping, reviewing implementation plans, documenting deviations, preparing handoffs, or deciding what context an agent needs.
license: MIT
---

# Find Unknowns

Behavioral guidelines to reduce agentic coding failures caused by missing context, derived from [Thariq Shihipar's field guide](https://x.com/trq212/status/2073100352921215386) on finding your unknowns.

**Tradeoff:** These guidelines bias toward clarification before execution. For trivial tasks, use judgment.

## 1. Map the Unknowns

**The prompt is the map. The codebase, product, users, and constraints are the territory. Make the gap explicit.**

Before implementing:
- List known knowns: facts already in the prompt, spec, code, or stated constraints.
- List known unknowns: questions you know must be answered.
- List unknown knowns: standards you would recognize only after seeing a prototype, diff, design, or behavior.
- Ask for unknown unknowns: blind spots, prior art, edge cases, hidden risks, or better possible outcomes.

If the unknowns dominate the task, do not execute immediately. Discover, interview, prototype, or inspect references first.

## 2. Discover Before Coding

**Find cheap unknowns before they become expensive code.**

Use the smallest artifact that exposes the uncertainty:
- Ask for a blindspot pass when the territory is unfamiliar.
- Ask the agent to teach you the domain vocabulary, quality bar, and failure modes when you cannot yet judge "good."
- Generate multiple concrete prototypes when you will only know the right answer after seeing it.
- Let the agent interview you one question at a time, prioritizing answers that would change architecture, APIs, data models, UX, or safety boundaries.
- Point at source code, examples, screenshots, docs, or prior implementations when words are too vague.
- Request a tweakable plan that leads with decisions you are likely to change and buries mechanical work.

For multi-step tasks, state the discovery loop:
```
1. [Artifact] -> reveals: [unknown]
2. [Question] -> changes: [decision]
3. [Plan] -> verify: [check before coding]
```

## 3. Track During Implementation

**Some unknowns only appear in the territory. Capture them instead of letting them disappear.**

During ambiguous or long-running work:
- Keep an `implementation-notes.md` or `.html` scratch artifact.
- When reality forces a deviation, choose the conservative path, log it under `Deviations`, and explain the evidence.
- If a new unknown invalidates the plan, stop and surface the decision instead of silently pivoting.
- Convert discovered facts into the next prompt, spec, checklist, test, or project instruction.

The test: a future attempt should start with a better map than the current attempt did.

## 4. Close the Loop

**Shipping means other people inherit your unknowns. Make them reviewable.**

Before merge, handoff, or approval:
- Package the prototype, spec, decisions, implementation notes, and evidence into a concise explainer.
- Lead with the demo or behavior, then answer the objections reviewers are likely to raise.
- Ask for a quiz or review guide when the change is too large to understand from the diff alone.
- Merge only when the owner understands what changed, why it changed, and what risks remain.

Strong closeout turns discovered unknowns into durable context. Weak closeout leaves the next agent or reviewer guessing again.
