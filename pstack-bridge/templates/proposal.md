## Why

<!--
Motivation for this change. What problem does this solve? Why now?

OpenSpec hard limit: 50 <= character count <= 1000.
- Too short: "Why section must be at least 50 characters" error
- Too long: "Why section should not exceed 1000 characters" error

Suggested shape: current pain -> why handle it now -> expected gain,
one or two sentences each.
-->

## What Changes

<!--
Describe what will change. Be specific about new capabilities,
modifications, or removals.

For behavior changes with a clear before/after, use From/To:

**<Section or Behavior Name>**
- From: <current state>
- To: <future state>
- Reason: <why this change is needed>
- Impact: <breaking / non-breaking, who is affected>

Repeat the block per change. Pure additions or deletions can use a
simple list.
-->

## Capabilities

### New Capabilities
<!--
Capabilities being introduced. Replace <name> with a kebab-case
compound noun (at least 2 words), e.g. `user-auth`, `data-export`,
`api-rate-limiting`. Each creates specs/<name>/spec.md.
-->
- `<name>`: <brief description of what this capability covers>

### Modified Capabilities
<!--
Existing capabilities whose REQUIREMENTS are changing (not just
implementation). Only list here if spec-level behavior changes.
Each needs a delta spec file. Use the existing spec name from
openspec/specs/. Leave empty if nothing changes.
-->
- `<existing-name>`: <what requirement is changing>

## Impact

<!-- Affected code, APIs, dependencies, systems. -->
