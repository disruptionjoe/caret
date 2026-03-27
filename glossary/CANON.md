# Canon Terms

These terms are stable enough to use across the repo.

## Core Notation Terms

`directive`
: A Caret^ signal such as `^depth8`, `^review`, or `^skeptical7`.

`scalar`
: A directive that varies by level, usually on the `0-9` convention.

`operational directive`
: A directive that signals a kind of work, such as `^review`, `^plan`, or `^audit`.

`target`
: The named or exact handle attached to `^^` or `^^^`.

`binding`
: The colon form that binds a directive to a target list, as in `^^review:critic`.

`count form`
: A bare number after `^^` or `^^^`, as in `^^3` or `^^^3`.

## Boundary Terms

`worker`
: The acting agent, process, or responsibility holder.

`hat`
: The lens, persona, stance, or loaded skill applied to the current worker.

`worker boundary`
: The point where responsibility shifts to a separate worker rather than a new lens on the same worker.

`fresh-eyes boundary`
: A `^^^^` section where prior context is cleared, discarded, or strongly deprioritized for what follows.

`enclosing scope`
: The parent block outside the current nested block. When a `^^^^` section closes, control returns here.

## Resolution Terms

`named target`
: A target expressed as a label or role name, such as `critic` or `researcher`.

`exact target`
: A target expressed as a precise handle, usually a repo-relative file path such as `personas/critic.md`.

`persona`
: A reusable lens or role description that can be applied as a hat or loaded by a harness.

`skill`
: A reusable instruction artifact that shapes how work is performed.

`harness`
: The runtime, prompt system, or execution layer that interprets Caret^.

`target resolution`
: The harness process that decides whether a target can actually be found and applied.

## Scope Terms

`scope`
: The block of text controlled by a directive.

`ambient directive`
: A broader directive already in effect for the current block.

`local override`
: A more specific directive in narrower scope or later position that overrides an ambient directive for the same dimension.

## Safety Terms

`trusted instruction space`
: Text the harness is expected to treat as live guidance.

`literal text`
: Text that should be preserved as text rather than interpreted as live instruction.

`promotion`
: The explicit act of moving text from literal or weak-trust space into trusted instruction space.
