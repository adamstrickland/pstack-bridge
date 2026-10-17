# Retrospective: <change-name>

> Written: <YYYY-MM-DD> (after verify passed)
> Commit range: `<base-sha>..<head-sha>`
> Worktree: <path or "merged to main">

---

## 0. Evidence

> Quantitative front-matter. Downstream Wins / Misses bullets cite
> §0 instead of repeating [evidence: ...] per line. A cold-write
> scenario (retro written days later) should be reconstructable
> from `git log` + `tasks.md` + commit messages alone.

- **Commit range**: `<base-sha>..<head-sha>` (<n> commits)
- **Diff size**: <+X / -Y lines across N files>
- **Tasks done**: <x>/<y> (`grep -cE '^\s*- \[x\]' tasks.md` -> x)
- **Active hours**: <estimate>
- **Subagent dispatches**: <count or "n/a">
- **New external dependencies**: <list with license + version, or "none">
- **Bugs encountered post-merge**: <count, one-line each, or "none">
- **OpenSpec validate state at archive**: <pass / fail / not-run>
- **Test coverage signal**: <e.g. pytest count, vitest count, or "n/a">
- **Decision-trail rows (pstack:show-me-your-work)**: <count, or "n/a - not required this cycle">

Commit chain (chronological):

```
<base-sha> <one-line summary>
...
<head-sha> <archive commit one-line>
```

---

## 1. Wins

- <description> (cf. §0 commit `<sha>` / file `<path>`)

## 2. Misses

- 🔴 [blocking] <description>
- 🟡 [painful]  <description>
- 📌 [nit]      <description>

## 3. Plan deviations

| Plan step | What changed | Why |
|-----------|--------------|-----|
| 1.2       | ...          | ... |

## 4. Skill / workflow compliance

| Skill                                | Used |
|--------------------------------------|------|
| pstack:sharpen                       |      |
| pstack:in-your-own-words             |      |
| pstack:architect                     |      |
| pstack:poteto-mode                   |      |
| pstack:show-me-your-work (optional)  |      |
| pstack:reflect                       |      |
| pstack:make-pr-easy-to-review        |      |

> **Default expectation**: every row checked. Each skill is in the
> flow for a reason. A row unchecked must be explained in
> `### Deliberately Skipped Skills` below.

### Deliberately Skipped Skills

> Skipping a skill is the escape hatch, not the common path. Each
> unchecked skill above must answer three questions. If this section
> is empty, every row above is checked (the default).

- **`<skill name>`**
  - **What was skipped**: <entire skill, or a specific sub-step>
  - **Why this cycle**: <concrete trigger. Vague reasons like "not
    needed", "too small", "no time", "blocked by external dep",
    "output looked off" are insufficient. Name the actual trigger
    (specific commit hash, log line, or observed behavior).>
  - **How to prevent recurrence**: pick one:
    - `schema graph fix` - name the schema.yaml section to change
    - `skill description tightening` - name the skill's frontmatter / instruction section
    - `CLAUDE.md trigger` - name the adopter CLAUDE.md.fragment section to add
    - `scope-judgment rule` - name the cycle-scoping rule
    - `one-off - schema boundary case` - explain why it is a boundary

> Multiple cycles skipping the same skill with similar prevention
> answers = §6 Promote candidate (schema or skill PR motivator).

## 5. Surprises

- <assumption that turned out wrong>

## 6. Promote candidates -> long-term learning

Each candidate is a `- [ ]` item:

- Title with severity emoji (🔴 / 🟡 / 📌) + one-sentence learning
- `-> **Promote to** <destination>` (memory / CLAUDE.md / schema / skill / one-off)
- Two body lines mirroring the feedback memory schema:
  - `> **Why**: <reason, often a past incident or strong preference>`
  - `> **How to apply**: <when / where this guidance kicks in>`

Unchecked `- [ ]` items carry forward to the next retro for
re-evaluation.

Examples:

- [ ] 🔴 **<short rule>** -> **Promote to memory** (type: feedback)
  > **Why**: <past incident or strong preference>
  > **How to apply**: <which file / cycle phase / decision moment>

- [ ] 🟡 **<another candidate>** -> **Promote to project CLAUDE.md** (`<path/to/CLAUDE.md>` section)
  > **Why**: ...
  > **How to apply**: ...

- [ ] 📌 **<third candidate>** -> **One-off** (record only, do not promote)
  > **Why**: <why it does not generalize>
