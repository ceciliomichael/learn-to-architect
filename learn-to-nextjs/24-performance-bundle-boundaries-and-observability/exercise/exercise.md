# Exercise: Performance, Bundle Boundaries, and Observability

1. Recreate the focused example in a disposable Next.js project.
2. Change the visible content and data while preserving the module rule.
3. Add the normal, empty, invalid, loading, or error state relevant to this lesson.
4. Test keyboard use and inspect the rendered DOM rather than checking appearance alone.
5. Explain which code owns state, external work, cleanup, and recovery.

## Success check

The project passes strict type checking and its behavior demonstrates this rule: Measure server work, client bundle size, navigation, rendering, and failures before optimizing. Keep interactive client boundaries small and attach logs or traces to request context without recording secrets.