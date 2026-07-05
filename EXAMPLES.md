# Examples

Real-world examples demonstrating the four principles. Each example shows what agents commonly do wrong when unknowns are left implicit and how to fix it.

---

## 1. Map the Unknowns

### Example 1: Hidden Task Boundaries

**User Request:** "Add a new auth provider"

**What agents often do:**

```text
Implement OAuth flow, create tables, add routes, update UI, and wire callbacks.
```

**Problems:**
- Assumed which auth module owns providers
- Assumed OAuth is the right protocol
- Assumed user linking semantics
- Assumed no migration or security review is needed

**What should happen:**

```text
Before implementing, map the unknowns:

Known knowns:
- Need a new auth provider.
- This codebase already has auth modules.

Known unknowns:
- Which provider?
- Should users link existing accounts or create new ones?
- Which module owns provider configuration?

Unknown knowns:
- Local code style and security patterns I will recognize after inspecting auth code.

Unknown unknowns:
- Existing callback edge cases, account takeover risks, migration history, provider-specific constraints.

I will inspect the auth modules and do a blindspot pass before proposing implementation.
```

---

## 2. Discover Before Coding

### Example 1: "I'll Know It When I See It"

**User Request:** "Make this dashboard feel more premium"

**What agents often do:**

```text
Pick one visual style, rewrite components, and hope the user likes it.
```

**Problems:**
- "Premium" is an unknown known
- The user may only recognize the right style after seeing options
- Implementation before prototype makes rollback expensive

**What should happen:**

```text
I will create four lightweight design directions before touching production code:

1. Dense operator console
2. Editorial analytics report
3. Financial terminal
4. Calm executive dashboard

Each prototype will include steal/skip notes so the user's reaction becomes a better implementation prompt.
```

---

## 3. Track During Implementation

### Example 1: Mid-Run Deviation

**Initial Plan:** "Port the Rust retry behavior into the TypeScript API client."

**What agents often do:**

```text
Discover the TypeScript client lacks request cancellation, silently omit cancellation behavior, and keep going.
```

**Problems:**
- The implementation now differs from the reference
- The deviation is invisible in the final diff
- The next attempt starts from the same weak map

**What should happen in `implementation-notes.md`:**

```markdown
# Implementation Notes

## Deviations

- The Rust reference cancels in-flight retries when a caller drops the future.
- The TypeScript client has no existing cancellation primitive.
- Conservative choice: preserve retry timing and error semantics, but do not invent cancellation support in this change.
- Follow-up decision: decide whether to add AbortSignal support before matching cancellation semantics.
```

---

## 4. Close the Loop

### Example 1: Review Handoff

**Finished Work:** "Export flow changed across 14 files"

**What agents often do:**

```text
Summarize the diff and say tests pass.
```

**Problems:**
- Reviewers inherit the same unknowns the implementer had
- Behavior is spread across existing code paths
- The owner may not understand the change deeply enough to merge it

**What should happen:**

```text
Create a review explainer:

1. Lead with a demo GIF or behavior summary.
2. Show the final user flow.
3. List the decisions made and alternatives rejected.
4. Link each risk to evidence: test, log, code path, or manual check.
5. Add a short quiz the owner must be able to answer before merging.
```

**The test:** The reviewer can explain what changed, why it changed, and what risk remains without reconstructing the whole diff.
