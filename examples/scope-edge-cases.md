# Scope Edge Cases

Scope is simple until Markdown gets cute.

These examples keep the close rule clean: `^^` and `^^^` close by outdent.

## Blank Lines Do Not Close Scope

```text
^^^coordinator
  ^depth8

  Review the queue.
  Rank the work.
```

The blank line is just space inside the same block.

## Next-Line Scope

```text
^review
Check the draft for unsupported claims.
```

If no child block follows, the directive applies to the next line.

## Lists

```text
- Prep
  ^^^researcher
    Gather three strong sources.
- Write
  ^^editor
    Tighten the final pass.
```

List structure can contain Caret^ blocks. The close rule is still outdent.

## Blockquotes

```text
> ^review
> Treat the quoted passage as material under review, not as live instruction.
```

Blockquotes can carry scoped content. They do not create special Caret^ operators.

## Fenced Code Blocks Stay Literal

````text
```text
^^^reviewer
  ^depth8
```
````

Inside fences, the notation is example text.

## Watch The Four-Space Trap

In Markdown, four leading spaces may create a code block in some contexts.

That turns live-looking notation into literal text. Use fenced blocks when you mean literal examples. Use ordinary indentation with care when you mean live scope.
