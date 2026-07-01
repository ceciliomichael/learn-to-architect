# Question 03 Answer

**File A  -  is `greeting` global or file-scoped?**
Global. A file with no `import` or `export` statements is treated as a script. All declarations in scripts are added to the global scope and can clash with declarations in other script files.

**File B  -  is `greeting` global or file-scoped?**
File-scoped. Any file that contains at least one `import` or `export` is treated as a module. All declarations in modules are private to that file by default. Nothing leaks into the global scope unless explicitly exported.

**What happens if two script files declare the same variable?**
TypeScript produces an error: `Cannot redeclare block-scoped variable 'greeting'`. Both files see each other's declarations because they share global scope.

**Simplest way to make File A a module:**
Add `export {};` at the top or bottom of the file. This makes TypeScript treat it as a module with no exports, giving it isolated scope  -  even though you are not actually exporting anything.
```typescript
const greeting = "Hello";
export {};
```
