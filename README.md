# pstack-bridge

An [OpenSpec](https://github.com/Fission-AI/OpenSpec) schema that bridges OpenSpec's artifact governance with [pstack](https://github.com/michael-denyer/pstack-claude)'s execution skills. Modeled on [JiangWay/openspec-schemas](https://github.com/JiangWay/openspec-schemas)' `superpowers-bridge`.

Each schema is a self-contained bundle you copy into your project's `openspec/schemas/` directory and select per-change with `--schema <name>`.

## Bridges in this repository

| Bridge | Purpose | Status |
|--------|---------|--------|
| [`pstack-bridge`](./pstack-bridge/) | Bridges OpenSpec with pstack skills (sharpen, architect, poteto-mode, reflect, show-me-your-work, make-pr-easy-to-review). Adds an evidence-first `retrospective` artifact. | v1 |

## Install

Each bridge directory has its own `README.md` with a copy-paste Claude Code prompt for one-shot installation, plus a manual bash alternative. See [`pstack-bridge/README.md#install`](./pstack-bridge/README.md#install).

## Why a separate repository

Follows the same reasoning as [JiangWay/openspec-schemas](https://github.com/JiangWay/openspec-schemas):

- OpenSpec core does not take on pstack's release cadence.
- The bridge iterates independently of pstack.
- Future community schemas can live here as siblings.

## License

MIT - see [LICENSE](./LICENSE).
