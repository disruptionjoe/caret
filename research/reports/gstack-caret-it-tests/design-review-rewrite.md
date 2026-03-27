# /design-review

Inherit the standard gstack runtime contract unchanged:

- preamble
- voice
- AskUserQuestion format
- completeness principle
- repo ownership rules
- search-before-building rule
- contributor mode
- completion status protocol
- telemetry
- plan status footer

Convert the skill-specific operating layer.

^design-review ^depth8 ^verification9 ^grip8
Audit a live site, fix what matters, verify each fix, and leave a report with evidence.

## Setup

^setup
Parse:

- target URL
- scope
- depth
- auth

Rules:

- if no URL and on a feature branch -> use diff-aware mode
- if no URL and on main/master -> ask for a URL
- if CDP mode is active -> skip cookie-import workarounds
- if a design system doc exists -> read it first

## Bootstrap

^bootstrap
Before any browse command:

- verify browse connectivity
- if no test framework exists and no opt-out marker exists, bootstrap one
- create `TESTING.md` and update `CLAUDE.md`
- commit the bootstrap separately

Keep framework detection, install commands, and CI steps literal from the source.

## Audit Modes

^mode

- full
- quick
- deep
- diff-aware
- regression

## Audit Flow

^first-impression
Capture the first screen. Grade composition, clarity, hierarchy, trust, and obvious AI-slop signals.

^extract-design-system
Record fonts, palette, heading hierarchy, touch targets, and performance baseline.

^audit-pages
Walk the selected pages and evaluate:

- visual hierarchy
- typography
- spacing and layout
- color and contrast
- interaction states
- responsive behavior
- content quality
- AI slop
- motion
- performance feel

^review-flows
Walk key user flows and judge the feel, not just the function.

^check-consistency
Compare cross-page rhythm, navigation, component reuse, and tone.

^compile-report
Write the structured audit report, baseline JSON, screenshots, findings, scores, and quick wins.

Keep scoring tables, output paths, and the design-hard-rules corpus literal from the source.

## Fix Loop

^triage
Sort findings by impact:

- high impact
- medium impact
- polish
- deferred

^fix-loop
For each fixable finding:

1. locate the source
2. make the smallest effective fix
3. commit one fix per commit
4. re-test with before/after screenshots
5. classify as verified, best-effort, reverted, or deferred

^regression-tests
Only generate regression tests for JavaScript behavior changes. Skip for CSS-only fixes.

^self-regulate
Track design-fix risk. Stop and ask if risk crosses the defined threshold or the fix count hits the cap.

## Close

^final-audit
Re-run the audit on affected pages. Warn if scores regress.

^report
Write:

- total findings
- fixes applied
- deferred findings
- design score delta
- AI slop score delta
- PR summary line

^todos
If `TODOS.md` exists, add deferred design findings and annotate any design items fixed in this run.

## Literal Surfaces To Preserve

Keep these literal in the full implementation:

- shell commands
- screenshot commands
- responsive commands
- report JSON schema
- score tables
- AI slop blacklist
- design hard rules
- output directory layout
