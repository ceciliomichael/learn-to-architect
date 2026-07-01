# Question 03 Answer

**Does it execute at runtime?**
No. `typeof serverConfig` inside a type declaration is a purely compile-time operation. The TypeScript compiler reads the type of `serverConfig` from the source code during compilation and uses it to define `ServerConfig`. The compiled JavaScript output contains no trace of this type extraction. It is completely erased.

This is different from the runtime `typeof` operator (`if (typeof x === "string")`), which does execute in JavaScript when the program is running.

**Exact type of `ServerConfig`:**
```typescript
{
  host: string;
  port: number;
  secure: boolean;
}
```

**Practical scenario:**
When you receive a configuration object from a library or environment that does not ship TypeScript types. Instead of manually writing an interface that might drift out of sync with the actual object, you use `typeof` to extract the type directly from the source. The type stays automatically accurate  -  if the object changes, the type changes with it.
