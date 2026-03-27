# /ship

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

Convert the ship workflow layer.

^ship ^verification9 ^precision9 ^grip9
Merge the base branch, verify the branch, review the diff, version it, push it, and open the PR or MR.

## Detect

^detect-platform
Detect:

- hosting platform
- base branch
- default fallbacks

Print the base branch and use it everywhere afterward.

## Pre-Flight

^preflight

- confirm review readiness
- check the distribution pipeline
- merge the base branch before tests

## Test Readiness

^bootstrap-tests
If test infrastructure is missing and no opt-out marker exists, bootstrap it.

Keep framework detection, install commands, CI setup, and `TESTING.md` generation literal from the source.

## Verification Pass

^run-tests
Run tests against merged code.

^triage-failures
Classify failures as:

- in-branch
- pre-existing

Route accordingly.

^evals
Run eval suites when the diff calls for them.

^coverage-audit
Audit affected-path coverage and generate missing tests when required.

^plan-audit
Cross-check implementation items, test items, and migration items against the current plan file.

^plan-verification
If the plan includes verification instructions and the environment supports them, run the verification pass.

## Review Stack

^pre-landing-review
Run the diff-scoped review.

^design-review
Run the conditional design review when frontend files changed.

^greptile
Address external review comments when a PR already exists.

^adversarial-review
Scale the adversarial pass by diff size.

Keep review prompts, gate logic, and dashboard templates literal from the source.

## Release Prep

^version
Auto-decide the bump level. Ask only for minor or major cases.

^changelog
Enumerate every commit, group by theme, and write a unified changelog entry that covers all substantive work.

^todos
Update `TODOS.md` conservatively based on clear diff evidence.

^commit
Split the work into bisectable commits. Reserve the metadata commit for version and changelog.

^verification-gate
If code changed after the earlier test run, re-run verification before push. No stale evidence.

## Publish

^push
Push the branch with upstream tracking.

^pr
Create the PR or MR with:

- summary
- test coverage
- pre-landing review
- design review
- eval results
- greptile review
- plan completion
- verification results
- todos
- test plan

Keep body templates and exact commands literal from the source.

^docs
Auto-run the documentation sync workflow and push docs updates if needed.

^metrics
Persist ship metrics for retro tracking.

## Literal Surfaces To Preserve

Keep these literal in the full implementation:

- git commands
- platform detection commands
- PR and MR body templates
- review prompts
- coverage diagrams
- metrics logging commands
- exact gate logic
