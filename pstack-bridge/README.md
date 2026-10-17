# pstack-bridge Schema

> Bridges [OpenSpec](https://github.com/Fission-AI/OpenSpec)'s artifact
> governance (the **what**) with [pstack](https://github.com/michael-denyer/pstack-claude)'s
> execution skills (the **how**) into a single workflow. Adds an
> evidence-first `retrospective` artifact filling a gap pstack does
> not natively cover.
>
> The integration lives at the prompt layer. No pstack source is
> modified. No OpenSpec CLI changes are required. Schema version: v1.

---

## Install

### Method 1: Claude Code one-shot prompt (recommended)

Paste into Claude Code at your project root:

```
Install the pstack-bridge schema for OpenSpec into this project:

1. Verify the project has an `openspec/` directory (run `openspec init` if missing).
2. Clone https://github.com/<owner>/pstack-bridge to a temp dir.
3. Copy the `pstack-bridge/` subdirectory to `openspec/schemas/pstack-bridge/`.
4. Run `openspec schema validate pstack-bridge` to verify.
5. Run `openspec schemas` and confirm `pstack-bridge` is listed.
6. Append `pstack-bridge/templates/adopters/CLAUDE.md.fragment.md` to this project's CLAUDE.md.
7. Confirm the pstack plugin is installed and these skills resolve:
   pstack:sharpen, pstack:in-your-own-words, pstack:architect,
   pstack:poteto-mode, pstack:show-me-your-work, pstack:reflect,
   pstack:make-pr-easy-to-review.
```

### Method 2: Manual bash

```bash
cd /tmp && git clone https://github.com/<owner>/pstack-bridge.git
cp -r /tmp/pstack-bridge/pstack-bridge /path/to/your/project/openspec/schemas/
cd /path/to/your/project
openspec schema validate pstack-bridge
cat openspec/schemas/pstack-bridge/templates/adopters/CLAUDE.md.fragment.md >> CLAUDE.md
```

Then select the schema per change with `--schema pstack-bridge` on `openspec` commands that support it, or wire it in as your default per OpenSpec's docs.

---

## What this bridge does

OpenSpec defines a change lifecycle (brainstorm -> proposal -> specs -> tasks -> plan -> apply -> verify -> archive) and enforces artifact structure (`### Requirement:`, `#### Scenario:`, delta spec deltas, `openspec validate`).

pstack-bridge keeps every OpenSpec artifact exactly where OpenSpec expects it, and tells the agent **which pstack skill to invoke to produce that artifact**:

| OpenSpec artifact | pstack skill invoked |
|---|---|
| `brainstorm.md` | `pstack:sharpen` + `pstack:in-your-own-words` + `pstack:architect` |
| `proposal.md` | prose extraction from brainstorm.md |
| `design.md` | prose reorganization of brainstorm.md |
| `specs/<cap>/spec.md` | prose, standard OpenSpec delta format |
| `tasks.md` | prose checklist, standard OpenSpec format |
| `plan.md` | prose, pstack-shaped (names data shape + playbook hint) |
| apply phase | `pstack:poteto-mode` (routes to the right playbook) |
| `verify.md` | checks per template; applies `principle-prove-it-works` |
| `retrospective.md` | `pstack:reflect` + optional `pstack:show-me-your-work` TSV |
| finishing | `pstack:make-pr-easy-to-review` + runtime PR skill |

On archive, delta specs sync into `openspec/specs/<cap>/spec.md` and the change folder moves to `openspec/changes/archive/YYYY-MM-DD-<name>/` using unchanged OpenSpec CLI behavior.

---

## Why pstack-bridge differs from superpowers-bridge

Both bridges follow the same shape. Where they diverge is what pstack mandates versus what superpowers mandates:

| Topic | superpowers-bridge | pstack-bridge |
|---|---|---|
| Apply executor | `subagent-driven-development` (fans out one subagent per micro-task) | `pstack:poteto-mode` (routes to a pstack playbook) |
| TDD | Mandatory (transitive through subagent-driven-development) | Opt-in - pstack's `tdd` skill is explicitly "use only when the user asks or the bug has a cheap local test target" |
| Code review | Mandatory (transitive) | Playbook-driven. Feature playbook calls `interrogate` when the design is contested. Opening-a-PR can call `thermos` / `thermo-nuclear-review` on demand. |
| Subagent platforms | Required | Not required - poteto-mode falls back to a single-agent execution |
| Retrospective | `openspec-verify-change` for verify + inline retro section | `pstack:reflect` (parallel reviewers) + optional show-me-your-work TSV folded into §0 Evidence |

The honest summary: superpowers-bridge enforces more. pstack-bridge trusts pstack's own routing. The schema stays small because `pstack:poteto-mode` already does the routing a schema would otherwise encode.

---

## Entry and exit gates

### Entry: when to use opsx vs direct PR

Use opsx when the change touches external contracts, schema, cross-system integration, or compliance. Direct-PR everything else (bug fixes without contract changes, test backfill, linter tweaks, non-breaking upgrades, typos, docs, config values).

### Exit: when verify can pass with warnings vs blocks

| verify.md section | Blocks archive? |
|---|---|
| 1. Structural validation | Yes |
| 2. Task completion (unfinished tasks without documented reason) | Yes |
| 3. Delta spec sync state (unsynced deltas) | Yes |
| 4. Design/specs coherence drift | No (warning) |
| 5. Implementation signal (uncommitted files) | Yes |
| 6. Verification surface check (wrong-surface or inconclusive) | Yes |
| 7. Decision-trail capture | No (warning, optional) |
| 8. Front-door routing leak | No (warning) |
| 9. Deferred dogfood equivalence missing when plan.md has `[~]` rows | Yes |

### Front-door routing leak

The brainstorm artifact routes `pstack:sharpen` / `pstack:architect` output into `openspec/changes/<name>/brainstorm.md`. If any content lands in `docs/pstack/specs/` or similar sibling directories, verify.md §8 flags it. Move the content into the change folder and delete the leak.

---

## Compatibility

- OpenSpec: tested against baseline 1.4.1 (same baseline as superpowers-bridge).
- pstack: tested against 0.9.92 (Claude Code port).
- Runtimes: Claude Code, Codex, Pi. No runtime-specific requirements beyond pstack itself.

---

## License

MIT - see [LICENSE](../LICENSE).
