# Skill: Convert Workflow to Notation-Backed Example

Take a real-world agent workflow described in prose and produce a field guide example that uses Caret^ notation.

## Input

A description of an agent workflow — what agents are involved, what they do, how context flows between them.

## Process

1. Identify the orchestration pattern (disposable specialists, perspective matrix, context refresh, routing, etc.)
2. Write the Caret^ notation version first
3. Add prose explanation of what each directive does in this context
4. Note which pattern from `field-guide/patterns/` this maps to
5. Flag anything the notation can't express yet (potential spec gaps)

## Output

A Markdown file suitable for `field-guide/examples/` with:
- Task description
- Caret^ notation block
- Prose walkthrough
- Pattern reference
- Optional: plain-language comparison showing what the notation replaces

## Voice

Match the repo voice: crisp, precise, no fluff. Show, don't explain.
