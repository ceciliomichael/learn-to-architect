# Module 15 Quiz Answers

## Answer 1

The optional property may be absent. The second property is required to exist, but its stored value may be undefined.

## Answer 2

`||` treats zero as false-like and uses the fallback. `??` uses the fallback only for null or undefined, so it preserves valid zero.

## Answer 3

No. It is a shallow static assignment rule. Runtime freezing and nested readonly types are separate concerns.

## Answer 4

It returns `undefined` instead of continuing the property access or method call.

## Answer 5

The key may not exist at runtime. Strict indexed access can reflect that as a union with undefined.
