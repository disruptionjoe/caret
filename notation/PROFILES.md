# Usage Profiles

Different contexts call for different subsets of the notation.

---

## File-first

The default. Caret notation lives in `.md` files — skills, CLAUDE.md, .cursorrules, agent configs. Full notation available. This is where Caret is most powerful.

<!-- TODO: document which constructs are file-first only -->

---

## Chat-safe

A subset safe for inline use in chat messages. No indentation-dependent semantics. No multi-line patterns. Just directives.

```
^depth7 ^temp3 ^grip8
```

One line. Works in any chat window.

<!-- TODO: define the exact chat-safe subset -->

---

## Minimal

The absolute minimum to start using Caret. Four symbols, one knob.

```
^    directive
^^   spawn ephemeral
^^^  spawn anchored
^^^^ clear context

^depth  how thorough (0-9)
```

If someone remembers nothing else, this is enough to get value.

<!-- TODO: validate that minimal profile is sufficient for common use cases -->
