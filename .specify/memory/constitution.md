<!--
Sync Impact Report
- Version change: none -> 1.0.0
- Modified principles: scaffold placeholders -> Code Quality, Testing Standards,
  Consistent User Experience, Performance
- Added sections: Quality Standards; Development Workflow
- Removed sections: none
- Follow-up TODOs: Confirm the original ratification date.
-->

# Flash Cards Constitution

## Core Principles

### I. Code Quality

Code MUST be clear, cohesive, and maintainable. New code MUST use existing project
patterns and abstractions where they fit, avoid unnecessary duplication, and keep
public interfaces minimal. Changes MUST handle expected errors explicitly and MUST
not introduce dead code, debug output, or unrelated refactoring. Rationale: a small
learning product needs a codebase that remains easy to change without making study
flows fragile.

### II. Testing Standards

As this is a pet-project, tests are not necessary unless actively asked for. They might be proposed to stabilyze the codebase or ensure a bugfix stays in the long run. Making sure the app respects the specification at all costs is the main testing strategy.

### III. Consistent User Experience

User-facing features MUST follow established navigation, terminology, visual
hierarchy, interaction, accessibility, and responsive-layout conventions. Shared
components and tokens MUST be reused instead of creating lookalike alternatives.
Loading, empty, success, error, and disabled states MUST be defined for each new
workflow. Keyboard access, readable contrast, and clear feedback MUST be preserved
across supported devices. Rationale: consistent interaction lowers cognitive load
and keeps attention on studying rather than operating the product.

### IV. Performance

Features MUST meet the performance budgets defined for their platform and workflow.
Implementations MUST avoid unnecessary network requests, rendering work, bundle
growth, and storage operations. Performance-sensitive changes MUST include a
measurement or benchmark when practical, and regressions MUST be investigated
before release. Core study interactions MUST remain responsive on supported mobile
and desktop devices. Rationale: latency interrupts recall practice and directly
reduces the product's usefulness.

### VI. Language

The specification will be written in english, but the application must be displaying text in french, in the french locale and timezone. 

**Version**: 1.0.0 | **Ratified**: 2026-09-05 | **Last Amended**: 2026-09-05
