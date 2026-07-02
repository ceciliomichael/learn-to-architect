# Question 03 Answer

**Why the compiler rejects this:**
```
Type 'number' is not assignable to type 'string'.
```

**Why TypeScript knew the type without an explicit annotation:**

This is called **type inference**. When you write `let city = "Tokyo"`, TypeScript looks at the value you assigned (`"Tokyo"`) and sees it is a string. From that moment on, TypeScript permanently associates the variable `city` with the type `string`  -  exactly as if you had written `let city: string = "Tokyo"`.

Type inference only works at the moment of assignment. Once TypeScript has inferred the type, it enforces it for the rest of the variable's life. Trying to assign `42` (a number) to `city` (which TypeScript knows is a string) is a type mismatch, which is exactly what the error says.

