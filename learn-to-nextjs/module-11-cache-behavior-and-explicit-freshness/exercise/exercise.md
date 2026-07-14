# Exercise: Cache Behavior and Explicit Freshness

1. Recreate the focused example in a disposable Next.js project.
2. Change the visible content and data while preserving the module rule.
3. Add the normal, empty, invalid, loading, or error state relevant to this lesson.
4. Test keyboard use and inspect the rendered DOM rather than checking appearance alone.
5. Explain which code owns state, external work, cleanup, and recovery.

## Success check

The project passes strict type checking and its behavior demonstrates this rule: Treat freshness as an explicit product decision. Know whether data can be reused, for how long, and what event makes it stale, then use the current cache and revalidation APIs deliberately.