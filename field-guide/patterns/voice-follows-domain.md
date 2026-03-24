# Voice Follows Domain

## Notation

```
^voice(domain)
```

The domain owns the voice. The agent borrows it.

## What it does

Routes output voice based on domain assignment, not agent identity. Caret^ domain gets Caret^ voice. Disruption Joe domain gets Disruption Joe voice. Same agent, different domains, different voices. The registry is the source of truth.

## When to use it

Every content assignment. Every output generation. Before the first word is written. Chief of staff consults the registry. No exceptions, no improvisation.

## When not to use it

Two structural exceptions exist. The Substack Rule: Joe's Substack uses Disruption Joe voice regardless of topic, because the platform is the domain, not the content subject. The Repo Rule: files living in a project repo use that project's native voice, not the chief's assignment. Both are recorded in decisions.md. Everything else follows the registry.

## Design notes

Voice is not personality. It is constraint. Constraint on tempo, sentence length, vocabulary, what gets said and what stays silent. A domain that requires Caret^ voice requires that particular constraint set. A domain that requires Disruption Joe voice requires a different constraint set. The agent is a tool that must fit the constraint.

The registry exists because human memory fails at scale. Written once, consulted always. When a new domain enters the system, the registry gets a new line. When domain properties change, the registry changes. No agent decides voice on the fly. No coordinator improvises. The registry is consulted; the decision is made.

The Substack Rule exists because platforms are domains. Joe's Substack is not a content domain, it is a platform domain. The platform owns the voice. Readers of the Substack expect Disruption Joe voice whether the topic is Caret^ orchestration or coffee preferences. This is not contradiction. This is hierarchy. Platform domain supersedes content domain.

The Repo Rule exists because repositories are live projects, not archives. A file living in the Caret^ repo is part of the Caret^ artifact. It must use Caret^ voice or it corrupts the artifact. A file living in the Joe EA repo must use that project's voice. Migration of a file between repos triggers voice conversion. This is work. Document it.

Related: Domain Anchor handles the assignment itself. Disposable Specialists inherit voice from domain, not from coordinator. When a specialist is rotated out, the voice stays because the domain stays.
