# Module 18 Quiz Answers

## Answer 1

A top-level `import` or `export` makes the file a module. An empty `export {};` can mark a file as a module when it has no other import or export.

## Answer 2

No. An unexported declaration remains inside its module.

## Answer 3

It makes clear that the name exists only for type checking and should not become a runtime import in emitted JavaScript.

## Answer 4

The runtime will load emitted `task.js`. TypeScript's Node-aware resolution relates that path to `task.ts` while checking source.

## Answer 5

Extra files can make navigation and relationships harder. A boundary should group a clear responsibility, not exist only to increase file count.
