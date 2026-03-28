# Emerging Terms

These terms are useful enough to track, but not stable enough to treat as canon.

They can appear in working docs. They should not quietly harden into spec language without a decision.

## Candidate Terms

`selected context`
: The subset of prior material a harness chooses to pass into a new worker.

`literal surface`
: A text region that should default to non-executable interpretation.

`promotion boundary`
: The point where copied or imported text is explicitly moved into trusted instruction space.

`target policy`
: The local rules a harness uses when resolving named or exact targets.

`directive strength`
: The practical force a harness gives a directive when it conflicts with prose, defaults, or safety policy.

## Harness-Layer Terms

`platform harness`
: Instructions that exist because of where the agent runs. Tool bindings, UI constraints, file path conventions, scheduling mechanisms. Change the platform, change this layer. Everything else stays.

`personal harness`
: Instructions that define who the agent is and how it behaves, regardless of platform. Decision frameworks, voice definitions, memory, principles, skill logic. Portable across platforms.

`project harness`
: Instructions scoped to a specific task, project, or domain. Context relevant now but not forever. Should not leak across projects.

`layer leakage`
: When instructions from one harness layer bleed into another. Platform-specific references in portable instructions. Project constraints that persist into unrelated work. Personal identity that thins because everything was pushed to platform or project layers. The failure mode that harness layering exists to prevent.

## Repo Rule

If one of these terms becomes necessary across multiple canonical docs, promote it deliberately through `/notation/DECISIONS.md`.
