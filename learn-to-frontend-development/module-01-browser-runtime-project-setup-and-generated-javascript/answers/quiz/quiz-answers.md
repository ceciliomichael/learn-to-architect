# Quiz Answers: Browser Runtime, Project Setup, and Generated JavaScript

1. **Why does the browser not execute TypeScript type annotations?**

   Browsers execute JavaScript; a compiler or development tool removes TypeScript-only syntax first.

2. **What should be committed as source?**

   The authored HTML, CSS, TypeScript, configuration, manifest, and reviewed lock file, not generated dependency folders.

3. **Why enable strict TypeScript?**

   It exposes missing null checks and unsafe assumptions before browser execution.

4. **What does a source map connect?**

   Generated JavaScript locations back to the authored source for debugging.

5. **Why use a local HTTP server?**

   Browser modules, URL resolution, and security policies behave more like deployment over HTTP than direct file loading.

