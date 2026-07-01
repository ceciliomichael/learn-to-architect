# Challenge 03: Solution

```typescript
interface ApiResponse<T = string> {
  success: boolean;
  data: T;
  errorMessage: string | null;
}

// Uses the default T = string. TypeScript infers .data as 'string'.
const textResponse: ApiResponse = {
  success: true,
  data: "Welcome to TypeScript!",
  errorMessage: null
};

// Uses T = number. TypeScript infers .data as 'number'.
const numberResponse: ApiResponse<number> = {
  success: true,
  data: 42,
  errorMessage: null
};

// Uses a custom object type.
const userResponse: ApiResponse<{ id: number; username: string }> = {
  success: true,
  data: { id: 1, username: "alice" },
  errorMessage: null
};

console.log(userResponse.data.username); // "alice"
```
