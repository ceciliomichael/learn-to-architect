# Exercise: Async Components, Loading, Error, and Empty States

1. Recreate the focused example in a disposable Vue project.
2. Change the visible content and data while preserving the module rule.
3. Add the normal, empty, invalid, loading, or error state relevant to this lesson.
4. Test keyboard use and inspect the rendered DOM rather than checking appearance alone.
5. Explain which code owns state, external work, cleanup, and recovery.

## Success check

The project passes strict type checking and its behavior demonstrates this rule: Async components can delay code loading, while data work needs explicit loading, empty, error, success, cancellation, and retry behavior.