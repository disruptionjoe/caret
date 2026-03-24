# Immutable State

## Notation

```
^ [protected files]
  ^^ [ephemeral agent]
    (works around, never modifies)
  ^^ [ephemeral agent]
    (works around, never modifies)
```

The caret stacked shows authority direction. Protected files sit above. Agents work below.

## What it does

Declares certain files as read-only to all agents. Not permission-based. Not soft. Hard walls. SKILL.md, skills/*.md, profile/*, brand-voice-guide.md, scripts/index.json, state.json. These files exist. Agents read them. Agents never change them.

Agents work around immutable state. They propose, defer, request human judgment. Or they create new files downstream. New data flows into new structures. Original structures stay clean.

## When to use it

When you need a stable reference layer that agents should treat as law. Your voice. Your profile. Your skill index. Your core state representation. When modification by an agent would corrupt the source of truth.

When you want agents to be creative within rails. Propose changes to you. Never sneak them in.

## When not to use it

When the file is genuinely mutable state. Logs. Caches. Temp work. Drafts. Those files should live elsewhere and be managed normally.

When you want full agent autonomy in a subsystem. Then don't protect it. Accept the risk.

## Design notes

Immutable state is a containment pattern. It forces a separation: read layer and write layer. You read law. You write proposals. Law never gets corrupted by proposals.

NIGHT-FACTORY demonstrates the cost clearly. Protected files are read-only. Agents cannot fix typos in SKILL.md even if they find one. They cannot update their own context record. They work around the friction. This is intentional. The friction buys you stability.

The pattern works because it's not abstract. You name exactly which files are protected. You update the protection list by hand. You own it. Agents don't negotiate. The protection is enforced by the system, not by agent honor code.

Consider three layers:

1. **Law layer** (immutable). SKILL.md, profile. These define you and the boundaries. Read-only.

2. **Working layer** (mutable). Drafts, proposals, observations, logs. Agents write here freely. You review.

3. **Archive layer** (immutable after closure). Completed work, decided items, historical record. You lock it once it's done.

This three-layer structure prevents the working layer from accumulating junk and the law layer from drifting. Immutable state isn't just security. It's a forcing function for good hygiene.

The trade-off is real. Immutable state costs agent speed. An agent cannot fix a broken index. An agent cannot update stale metadata. The agent must flag it, leave it broken, wait for you. This friction is the feature, not the bug. You buy stability by accepting that agents move slower around protected boundaries.

Hard implementation detail: the system that enforces immutability must be hostile to social engineering. An agent cannot convince you to "temporarily" unlock SKILL.md for a "quick fix". The file is locked. You unlock it with a separate explicit action. Same with scripts/index.json. Protected means protected.

Another detail: immutable state creates a clear audit trail. Who proposed a change. When. What they wanted to change. You can see the full history in the proposals without the noise of failed attempts to modify the source.

The pattern scales because it's binary. A file is protected or it isn't. No gradations. No "mostly protected". This simplicity is why it works. Agents understand walls. Agents work around walls. Agents don't understand "partially protected" and neither do you after six months of context rot.
