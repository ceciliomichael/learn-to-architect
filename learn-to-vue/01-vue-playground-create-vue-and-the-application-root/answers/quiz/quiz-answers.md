# Quiz Answers: Vue Playground, create-vue, and the Application Root

1. The playground provides a ready online environment. A local project exposes dependency installation, files, scripts, type checking, builds, and generated output.
2. `npm create vue@latest` downloads and runs the official `create-vue` generator.
3. Those features are taught later. Leaving them out avoids unexplained files and lets the learner add each dependency with understanding.
4. `index.html` provides the DOM mount element, `src/main.ts` creates and mounts the application, and `src/App.vue` defines its visible root component.
5. A browser can display code that still contains type errors elsewhere. Vue-aware type checking examines TypeScript used by scripts and component templates.
