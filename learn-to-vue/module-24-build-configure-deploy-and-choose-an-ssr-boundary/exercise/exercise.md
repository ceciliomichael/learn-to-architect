# Exercise: Build, Configure, Deploy, and Choose an SSR Boundary

1. Recreate the focused example in a disposable Vue project.
2. Change the visible content and data while preserving the module rule.
3. Add the normal, empty, invalid, loading, or error state relevant to this lesson.
4. Test keyboard use and inspect the rendered DOM rather than checking appearance alone.
5. Explain which code owns state, external work, cleanup, and recovery.

## Success check

The project passes strict type checking and its behavior demonstrates this rule: Build and type-check the production application, validate environment configuration, expose only public client values, test the deployed artifact, and choose SSR only when its server and hydration costs solve a real need.