# Exercise: Lifecycle Hooks and Template Refs

1. Recreate the focused example in a disposable Vue project.
2. Change the visible content and data while preserving the module rule.
3. Add the normal, empty, invalid, loading, or error state relevant to this lesson.
4. Test keyboard use and inspect the rendered DOM rather than checking appearance alone.
5. Explain which code owns state, external work, cleanup, and recovery.

## Success check

The project passes strict type checking and its behavior demonstrates this rule: Lifecycle hooks schedule work around component mounting and removal, while template refs provide limited DOM access after mounting. Clean up every owned external resource.