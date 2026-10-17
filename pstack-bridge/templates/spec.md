<!--
Delta spec template for a change.

Four delta section kinds, used as needed:
  ADDED / MODIFIED / REMOVED / RENAMED

File location: openspec/changes/<change-name>/specs/<capability>/spec.md
(`<capability>` matches openspec/specs/<capability>/ for MODIFIED /
REMOVED / RENAMED.)

OpenSpec hard rules (validate will enforce):
- Requirement sentence MUST contain `SHALL` or `MUST`.
- Every Requirement MUST have at least one `#### Scenario:` block.
- Scenario headers MUST be level 4 (`####`). Level 3 or bullets
  will silently fail validation.
-->

## ADDED Requirements

<!-- New behavior. List each Requirement being added to this capability. -->

### Requirement: <!-- requirement name -->
<!-- requirement text - MUST contain SHALL or MUST -->

#### Scenario: <!-- scenario name -->
- **WHEN** <!-- condition -->
- **THEN** <!-- expected outcome -->

---

## MODIFIED Requirements

<!--
Modify existing Requirements. The header MUST match the normalized
header in openspec/specs/<capability>/spec.md exactly (case-sensitive
after trim), or the archive-time delta apply will fail to find the
requirement.

MUST include the full updated content (not a diff). OpenSpec archive
applies MODIFIED as a whole-text replacement.
-->

### Requirement: <!-- same header as the existing spec -->
<!-- full updated requirement text - MUST contain SHALL or MUST -->

#### Scenario: <!-- scenario name (new or revised) -->
- **WHEN** <!-- condition -->
- **THEN** <!-- expected outcome -->

---

## REMOVED Requirements

<!--
Remove existing Requirements. MUST include Reason and Migration so
reviewers understand why it is retired and how callers should adapt.
-->

### Requirement: <!-- header to remove, must match existing spec exactly -->

**Reason**: <!-- why this is retired -->

**Migration**: <!-- how existing callers / consumers adapt -->

---

## RENAMED Requirements

<!--
Rename a Requirement header. Fixed format:
- FROM / TO as code-fenced headers.
- If the name changes AND the content changes, list it under
  RENAMED and ALSO under MODIFIED with the NEW header and full
  updated content.

Archive apply order: RENAMED -> REMOVED -> MODIFIED -> ADDED.
-->

- FROM: `### Requirement: <Old Name>`
- TO: `### Requirement: <New Name>`
