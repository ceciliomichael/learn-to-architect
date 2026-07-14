# Module 32 Exercises

## Exercise 1: Trace a package type

Choose one installed package. Use editor navigation and its `package.json` to determine whether its types are bundled or come from `@types`. Record the declaration entry and one exported function signature.

## Exercise 2: Declare a JavaScript module

Assume `simple-slug` exists at runtime and exports:

```javascript
export function slugify(text, lowercase = true) {
  const result = text.trim().replaceAll(" ", "-");
  return lowercase ? result.toLowerCase() : result;
}
```

Write a `.d.ts` module declaration with accurate parameter and return types.

## Exercise 3: Observe missing runtime code

Explain what happens if the declaration from Exercise 2 exists but the actual package is not installed.

## Exercise 4: Replace an empty declaration

Replace `declare module "simple-slug";` with the honest function declaration and explain what errors TypeScript can now catch.

## Exercise 5: Generate your own declaration

In a small project, export a function and interface, enable `declaration`, build, and inspect the emitted `.d.ts`. Confirm that an unexported helper is absent.

## Completion checklist

- [ ] I found the source of a package's types.
- [ ] I read a declaration from one exported name.
- [ ] I wrote a declaration matching runtime behavior.
- [ ] I kept type declarations separate from implementations.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
