# Question 02 Answer

**Does it error?**
No. TypeScript does not throw an error.

**What `void` means in a callback return type:**
When `void` appears as a callback return type, it does not mean the callback must return nothing. It means: "I do not care what this callback returns. I will not use the return value." TypeScript will simply ignore whatever the callback returns.

**Why TypeScript was designed this way:**
This is intentional. Consider `.forEach()`, which is defined as accepting a `(item: T) => void` callback. If TypeScript strictly enforced that the callback returns nothing, you could never pass a regular named function that happens to return a value to `.forEach()`. That would make many valid and common patterns impossible. By treating `void` callbacks permissively, TypeScript stays practical and compatible with real-world JavaScript patterns.
