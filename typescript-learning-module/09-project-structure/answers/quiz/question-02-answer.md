# Question 02 Answer

**Why they form a circle:**
`orderService.ts` imports from `logService.ts`. `logService.ts` imports from `orderService.ts`. Each file depends on the other. When Node.js tries to load `orderService`, it starts loading `logService`, which tries to load `orderService`  -  which is still in the middle of loading. The circle is: A needs B, B needs A.

**What might happen at runtime:**
Node.js detects the circular dependency and resolves it by providing a partially-initialized version of one of the modules  -  whatever has been defined so far at the point the cycle was detected. This often results in `undefined` being imported instead of the actual function. The code compiles without error but silently fails at runtime: `getOrderCount is not a function`.

**How to break the cycle:**
Move the shared dependency into a third file that neither service imports from the other to get:
```
services/
├── orderService.ts    -  imports from repositories/orderRepository.ts only
├── logService.ts      -  takes a message and count as parameters instead of calling orderService
└── utils/logger.ts    -  pure logging utility with no imports from other services
```
The general rule: higher-level modules can depend on lower-level modules, but lower-level modules must never depend back on higher-level ones. Types and utilities should flow downward, never in a loop.
