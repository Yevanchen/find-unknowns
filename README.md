# Thariq-Inspired Agent Unknowns Guidelines

[![skills.sh](https://skills.sh/b/Yevanchen/thariq-shihipar-skills)](https://skills.sh/Yevanchen/thariq-shihipar-skills/find-unknowns)

A single `CLAUDE.md` file to improve agentic coding behavior, derived from [Thariq Shihipar's field guide](https://x.com/trq212/status/2073100352921215386) on finding unknowns before, during, and after implementation.

English | [简体中文](./README.zh.md)

## The Problems

From Thariq's post:

> The prompt, skills, and context you give an agent are only a map of the work.

> The real territory is the codebase, the product, the real world, and the constraints that appear during implementation.

> When the map and territory diverge, the agent must guess what you wanted.

## The Solution

Four principles in one file that directly address these issues:

| Principle | Addresses |
|-----------|-----------|
| **Map the Unknowns** | Missing context, hidden assumptions, vague task boundaries |
| **Discover Before Coding** | Unknown unknowns, "I'll know it when I see it" requirements |
| **Track During Implementation** | Mid-run deviations, edge cases, silent pivots |
| **Close the Loop** | Reviewer confusion, weak handoffs, lost implementation context |

## The Four Principles in Detail

### 1. Map the Unknowns

**The prompt is the map. The codebase, product, users, and constraints are the territory. Make the gap explicit.**

Before implementing, break the task down:

- **Known knowns** — Facts already in the prompt, spec, code, or stated constraints
- **Known unknowns** — Questions you know must be answered
- **Unknown knowns** — Standards you would recognize only after seeing a prototype, diff, design, or behavior
- **Unknown unknowns** — Blind spots, prior art, edge cases, hidden risks, or better possible outcomes

If the unknowns dominate the task, do not ask the agent to execute immediately. Ask it to discover, interview, prototype, or inspect references first.

### 2. Discover Before Coding

**Find cheap unknowns before they become expensive code.**

Use the smallest artifact that exposes the uncertainty:

- **Blindspot pass** — Ask for relevant unknown unknowns when the territory is unfamiliar
- **Teach me my unknowns** — Ask for vocabulary, quality bars, and failure modes in a domain you cannot yet judge
- **Brainstorm or prototype** — Generate multiple concrete options when you will only know the right answer after seeing it
- **Interview** — Ask one question at a time, prioritizing answers that would change architecture, APIs, data models, UX, or safety boundaries
- **References** — Point at source code, examples, screenshots, docs, or prior implementations when words are too vague
- **Tweakable plan** — Lead with decisions the user is likely to change and bury mechanical work

**The test:** Did the artifact reveal a decision, risk, or quality bar before implementation started?

### 3. Track During Implementation

**Some unknowns only appear in the territory. Capture them instead of letting them disappear.**

During ambiguous or long-running work:

- Keep an `implementation-notes.md` or `.html` scratch artifact
- Log deviations under `Deviations` when reality forces a plan change
- Choose the conservative path when continuing without user input
- Stop and surface the decision if a new unknown invalidates the plan
- Convert discovered facts into the next prompt, spec, checklist, test, or project instruction

**The test:** Would a future attempt start with a better map than this attempt did?

### 4. Close the Loop

**Shipping means other people inherit your unknowns. Make them reviewable.**

Before merge, handoff, or approval:

- Package the prototype, spec, decisions, implementation notes, and evidence into a concise explainer
- Lead with the demo or behavior, then answer the objections reviewers are likely to raise
- Ask for a quiz or review guide when the change is too large to understand from the diff alone
- Merge only when the owner understands what changed, why it changed, and what risks remain

**The test:** Can the reviewer understand the work without reconstructing your unknowns from the diff?

## Install

**Option A: skills.sh / Agent Skills**

Install the reusable skill with the Skills CLI:

```bash
npx skills add Yevanchen/thariq-shihipar-skills --skill find-unknowns
```

Use it without installing:

```bash
npx skills use Yevanchen/thariq-shihipar-skills --skill find-unknowns
```

**Option B: Claude Code Plugin**

From within Claude Code, first add the marketplace:

```
/plugin marketplace add Yevanchen/thariq-shihipar-skills
```

Then install the plugin:

```
/plugin install thariq-shihipar-skills@thariq-skills
```

This installs the guidelines as a Claude Code plugin, making the skill available across your projects.

**Option C: CLAUDE.md (per-project)**

New project:

```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/Yevanchen/thariq-shihipar-skills/main/CLAUDE.md
```

Existing project (append):

```bash
echo "" >> CLAUDE.md
curl https://raw.githubusercontent.com/Yevanchen/thariq-shihipar-skills/main/CLAUDE.md >> CLAUDE.md
```

## Using with Cursor

This repository includes a committed Cursor project rule ([`.cursor/rules/find-unknowns.mdc`](.cursor/rules/find-unknowns.mdc)) so the same guidelines apply when you open the project in Cursor. See **[CURSOR.md](CURSOR.md)** for setup, using the rule in other projects, and how this relates to Claude Code.

## Key Insight

The quality bottleneck for strong coding agents is often not generation ability. It is whether the human and the agent have reduced the unknowns enough for the agent to make good decisions without guessing.

The "Find Unknowns" principles capture this: turn vague task context into artifacts, questions, plans, notes, and explainers that continuously align the map with the territory.

## How to Know It's Working

These guidelines are working if you see:

- **Fewer silent assumptions** — Unknowns are surfaced before implementation
- **Better plans** — Plans lead with decisions the user may tweak
- **Better long runs** — Deviations are logged instead of hidden
- **Better reviews** — Reviewers understand what changed, why, and what risks remain

## Customization

These guidelines are designed to be merged with project-specific instructions. Add them to your existing `CLAUDE.md` or create a new one.

For project-specific rules, add sections like:

```markdown
## Project-Specific Unknowns

- Ask for a blindspot pass before changing billing code
- Prototype visual changes before wiring backend behavior
- Log deviations in `implementation-notes.md` for any multi-hour task
```

## Tradeoff Note

These guidelines bias toward **clarification over speed**. For trivial tasks, simple typo fixes, and obvious one-liners, use judgment. Not every change needs the full unknowns workflow.

The goal is reducing costly mistakes on ambiguous work, not slowing down simple tasks.

## License

MIT
