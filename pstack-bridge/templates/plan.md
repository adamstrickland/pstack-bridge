# <Change name> Implementation Plan

> **For agents:** the apply phase hands this file to **pstack:poteto-mode**,
> which routes to the right pstack playbook (Feature / Bug fix /
> Refactoring / Perf issue / Visual parity / other). plan.md is a
> static document - no skill invocation here.

**Goal:** <!-- one sentence -->

**Data shape:**
<!--
Required. Name the data shape and its organizing structure before
any implementation step. This is pstack's foundational rule, from
the **principle-model-the-domain** principle skill.

Examples:
- A state machine over scattered booleans (name the states + transitions)
- A typed model over repeated shape assumptions (name the type)
- A table / registry over branching (name the key -> value shape)
- A reducer over mutation-at-a-distance (name the action set)
-->

**Playbook hint:** <!-- Feature | Bug fix | Refactoring | Perf issue | Visual parity | Other -->
<!--
poteto-mode may route differently if its own classification disagrees.
Hint is advisory; the executor owns the final routing decision.
-->

**Verification surface:** <!-- unit test | integration test | UI driver | CLI driver | manual dogfood -->
<!--
The matching surface per pstack Feature playbook step 5. "Inconclusive"
or wrong-surface is not a pass.
-->

---

## Steps

- [ ] 1. <!-- step description, with file paths and success criterion -->
- [ ] 2. <!-- step description -->
- [~] 3. <!-- step description -->  <!-- [~] marks a deferred dogfood / manual check. verify.md will enumerate equivalents. -->

<!--
Steps are coarse. Decomposition into micro-tasks (and whether to
drive each via a dedicated subagent) is poteto-mode's call based on
the matched playbook. The Feature playbook, for example, mandates a
code-writing delegate with its own worktree; the Refactoring
playbook may not.
-->
