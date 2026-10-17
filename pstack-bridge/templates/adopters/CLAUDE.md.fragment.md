<!-- Source: pstack-bridge/templates/adopters/CLAUDE.md.fragment.md -->
<!-- Drop this section into your project's CLAUDE.md so the agent routes future work using this schema correctly. -->
<!-- Adjust the schema name and bridge repo URL if you customized them; otherwise keep as-is. -->

## Workflow routing (read on session start)

This repo uses [`pstack-bridge`](https://github.com/<owner>/pstack-bridge/tree/main/pstack-bridge) to bridge OpenSpec and pstack. Integration rules (artifact paths, PRECHECK, apply executor) follow that bridge's README; this section is the routing guidance for the agent.

### Entry routing

| Trigger you observe | What to do |
|---|---|
| User asks for a design discussion / "let's brainstorm" / "sketch this" | Run verbal `pstack:sharpen` -> `pstack:in-your-own-words` -> `pstack:architect`. Do NOT write to `docs/pstack/specs/`. When the five promotion criteria below hold, suggest `/opsx:propose`. |
| User invokes `/opsx:new` / `/opsx:ff` / `/opsx:propose` directly | Follow the schema flow. Artifact instructions inject at each step. |
| User says bug fix / typo / config tweak / doc update | Direct PR. Do NOT open a change (see skip rules). |
| User is mid-change | Advance with `/opsx:continue`, `/opsx:apply`, `/opsx:verify`, or `/opsx:archive`. |
| User asks to ship / check CI / handle review comments on an existing PR | Route to the pstack **Babysit** playbook via `pstack:poteto-mode`, not to opsx. |

### When NOT to use opsx (direct PR)

| Scenario | Direct PR? |
|---|---|
| New feature / new capability / architectural change / breaking change | No - use opsx |
| Bug fix (no contract change) / test backfill / linter tweak / non-breaking upgrade / typo / docs / config value tweak | Yes - direct PR |

Principle: ceremony scales with risk. External contracts / schema / cross-system integration / compliance -> opsx. Otherwise -> direct PR.

### Verbal brainstorm -> opsx promotion criteria

All five must hold before promoting (any missing -> keep brainstorming, never write to `docs/pstack/specs/`):

1. **Scope locked** - one sentence covers in / out.
2. **Major design forks resolved** - alternatives weighed; remaining TBDs have an owner and impact-scope statement.
3. **Cross-system dependencies mapped** - ready / mockable / genuinely unknown, pick one per dep.
4. **Acceptance criteria stateable** - concrete pass conditions (e.g. `./test.sh` passes + N deliverables).
5. **Conversation converging** - recent turns are confirmations, not new alternatives.

When all five hold -> proactively suggest "ready to `/opsx:propose`?" and wait for user ack. Never auto-trigger.

### Front-door anti-patterns (do not do)

- Letting the sharpen / architect output write to `docs/pstack/specs/`.
- Letting plan.md land in `docs/pstack/plans/`.
- Promoting to opsx with unresolved blocking TBDs.
- Opening a change for bug fix / typo.

### Apply phase quick reference

- The apply phase hands plan.md to `pstack:poteto-mode`.
- poteto-mode routes to a pstack playbook (Feature / Bug fix / Refactoring / Perf issue / Visual parity / other) and does NOT force TDD.
- Verification runs on the surface named in plan.md's `Verification surface`.
- When the task meets its criteria (autonomous or multi-phase run, work a human reviews after stepping away), poteto-mode records a decision trail via `pstack:show-me-your-work`.
- Retrospective is written BEFORE opening the PR, via `pstack:reflect`.

Full detail: see the pstack-bridge README `#entry-and-exit-gates` section.
