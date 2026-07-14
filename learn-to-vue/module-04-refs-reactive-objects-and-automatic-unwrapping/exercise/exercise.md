# Exercise: Refs, Reactive Objects, and Automatic Unwrapping

1. Recreate the focused example in a disposable Vue project.
2. Change the visible content and data while preserving the module rule.
3. Add the normal, empty, invalid, loading, or error state relevant to this lesson.
4. Test keyboard use and inspect the rendered DOM rather than checking appearance alone.
5. Explain which code owns state, external work, cleanup, and recovery.

## Success check

The project passes strict type checking and its behavior demonstrates this rule: A ref owns one reactive value and a reactive object tracks its properties. Templates unwrap refs for convenient reading, while TypeScript code normally uses value.