# Question 02 Answer

```typescript
// Importing PI and square (named imports)
import { PI, square } from "./utils";

// Importing MathHelper (default import  -  no curly braces)
import MathHelper from "./utils";

// Both together
import MathHelper, { PI, square } from "./utils";
```

**Can you rename a named import? Syntax:**
Yes, using `as`
```typescript
import { square as computeSquare } from "./utils";
```

**Can you rename a default import? Syntax:**
Yes  -  with default imports, the name you choose in the import statement IS the name. There is no `as` needed because the caller decides the name
```typescript
import Calculator from "./utils";  // "Calculator" is your chosen name for the default.
```

**Can a file have multiple default exports?**
No. A file can have exactly one default export. The purpose of a default export is to declare "this is THE main thing this file provides." If you need to export multiple things, use named exports.
