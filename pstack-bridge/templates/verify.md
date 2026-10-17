# Verification Report

> Produced after apply completes. Re-run verify as often as needed;
> each run overwrites this file. Failing items block archive until
> the owning artifact is fixed.

**Change**: `<change-name>`
**Verified at**: `YYYY-MM-DD HH:mm`
**Verifier**: `<who / which agent>`

---

## 1. Structural Validation (`openspec validate --all --json`)

- [ ] All items return `"valid": true`

**Output summary:**

```text
<paste openspec validate --all output summary>
```

Failures (if any):

| Item | Type | Issues |
|---|---|---|
| — | — | — |

---

## 2. Task Completion (`tasks.md`)

- [ ] All `- [ ]` boxes converted to `- [x]`

Incomplete tasks (if any):

| Task | Reason unfinished | Blocks archive? |
|---|---|---|
| — | — | — |

---

## 3. Delta Spec Sync State

For each capability directory under `openspec/changes/<name>/specs/`,
compare against `openspec/specs/<capability>/spec.md`:

| Capability | Sync state | Notes |
|---|---|---|
| — | checkmark synced / unchecked pending / N/A | — |

---

## 4. Design / Specs Coherence Spot Check

Sample-check that design.md decisions appear in specs/ Requirements
and Scenarios:

| Sample | design.md statement | specs/ counterpart | Gap |
|---|---|---|---|
| — | — | — | — |

Drift warnings (non-blocking):

- <list, or "none">

---

## 5. Implementation Signal (principle-prove-it-works)

- [ ] Worktree has no unstaged files
- [ ] All relevant commits pushed
- [ ] Verified against the real artifact (feature run / value read /
      diff inspected), not a proxy or "it compiles"

Commit range (if known): `<from-sha>..<to-sha>`

---

## 6. Verification Surface Check

Matching surface named in plan.md: `<unit / integration / UI driver / CLI driver / dogfood>`

- [ ] That surface actually ran and produced a definitive verdict
- [ ] No "inconclusive" or wrong-surface results slipped through

If verification ran on the wrong surface, that is a FAIL per the
pstack Feature playbook. Return to the owning step before continuing.

---

## 7. Decision-Trail Capture (optional, warning only)

If pstack:show-me-your-work ran during apply:

- [ ] `.audit/<change-name>.tsv` (or project equivalent) exists
- [ ] One row per non-trivial decision, with evidence and result

Non-blocking. show-me-your-work is required only when the task meets
its own criteria (autonomous or multi-phase run, or work a human
reviews after stepping away).

---

## 8. Front-Door Routing Leak Detector (warning, non-blocking)

Design output must not land in `docs/pstack/specs/` or any sibling
directory outside the change folder. The brainstorm artifact's
instruction routes it to `openspec/changes/<name>/brainstorm.md`.

Check:

```bash
ls docs/pstack/specs/*.md 2>/dev/null
```

Leaked files (if any):

| File | Content already captured in change? | Suggested action |
|---|---|---|
| — | — | — |

> Non-blocking. Leaks from new schema-installed cycles should be
> moved into `openspec/changes/<name>/brainstorm.md` or `design.md`
> and the original deleted.

---

## 9. Deferred Dogfood vs Automated-Test Equivalence

For each `[~]` deferred step in plan.md, identify the equivalent
automated test. No equivalent = a real coverage gap, record in
retrospective Misses.

| Deferred step (plan §) | Equivalent automated test | Coverage assessment | Real gap? |
|---|---|---|---|
| — | — | — | — |

> When plan.md has no `[~]` rows, this section may be left empty
> (that is a PASS). If plan.md has `[~]` rows and this section is
> empty, Overall Decision must be FAIL.

---

## Overall Decision

- [ ] PASS — proceed to retrospective and archive
- [ ] PASS WITH WARNINGS — proceed, note: `<explanation>`
- [ ] FAIL — fix the owning artifact and re-run verify

**Next step:**

<describe the next action>
