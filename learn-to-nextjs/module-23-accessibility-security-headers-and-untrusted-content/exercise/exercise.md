# Exercise: Accessibility, Security Headers, and Untrusted Content

1. Recreate the focused example in a disposable Next.js project.
2. Change the visible content and data while preserving the module rule.
3. Add the normal, empty, invalid, loading, or error state relevant to this lesson.
4. Test keyboard use and inspect the rendered DOM rather than checking appearance alone.
5. Explain which code owns state, external work, cleanup, and recovery.

## Success check

The project passes strict type checking and its behavior demonstrates this rule: Preserve semantic HTML and keyboard behavior, apply security headers deliberately, validate untrusted content, and avoid rendering raw HTML unless it has a proven sanitization boundary.