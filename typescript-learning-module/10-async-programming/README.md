# Module 10: Async Programming - Promises and Async/Await

Almost everything meaningful in a real application involves waiting: waiting for a database query to finish, waiting for an API to respond, waiting for a file to load. TypeScript handles this with **asynchronous programming**. This module teaches you everything you need to write and understand async code confidently.

---

## 1. The Problem: Why Async Exists

Imagine your program asks a server for some user data. That request takes 2 seconds. Without async programming, your entire program would freeze for those 2 seconds, unable to do anything else. This is called **blocking**.

Async programming lets your program say: "Start this task, and when it is done, come back and handle the result. In the meantime, keep doing other things."

---

## 2. What is a Promise?

A `Promise` is an object that represents the eventual result of an asynchronous operation. When you start an async task, it immediately returns a Promise as a placeholder. The Promise can be in one of three states
- **Pending**: The task is still running. No result yet.
- **Fulfilled**: The task completed successfully. The Promise now holds the result.
- **Rejected**: The task failed. The Promise now holds an error.

### Typing a Promise

When you type a function that returns a Promise, you use `Promise<T>` where `T` is the type of the eventual result
```typescript
// This function returns a Promise that will eventually resolve to a string
function fetchUsername(): Promise<string> {
  return new Promise((resolve, reject) => {
    // Simulating a network delay of 1 second
    setTimeout(() => {
      resolve("Alice"); // The task succeeded. "Alice" is the result.
    }, 1000);
  });
}
```

The `resolve` function is called when the task succeeds. The `reject` function is called when it fails.

### `.then()` and `.catch()`

You can attach callbacks to a Promise to handle its result when it eventually arrives
```typescript
fetchUsername()
  .then((name) => {
    // 'name' is the resolved value: "Alice"
    console.log("Got user:", name);
  })
  .catch((error) => {
    // This runs if the Promise was rejected.
    console.log("Something went wrong:", error);
  });
```

This works but becomes messy when you chain multiple async operations. This is why `async/await` was created.

---

## 3. `async` and `await`: The Clean Way

`async` and `await` are special keywords that let you write async code that reads like normal, top-to-bottom synchronous code.

### `async` Functions

Adding `async` before a function declaration makes it an async function. An async function always returns a `Promise`, even if you return a plain value inside it
```typescript
async function getGreeting(): Promise<string> {
  return "Hello, World!"; // TypeScript wraps this in Promise<string> automatically.
}
```

### `await`

The `await` keyword pauses execution inside an async function until the Promise resolves. It then hands you the resolved value directly, without needing `.then()`
```typescript
async function showUser(): Promise<void> {
  const name = await fetchUsername(); // Pauses here until the Promise resolves.
  console.log("User is:", name);      // Then continues with the result.
  console.log("Done.");
}
```

This code looks like it runs from top to bottom, but it does not block the rest of the program. `await` only pauses inside the current async function.

### You Can Only Use `await` Inside an `async` Function

```typescript
// Top level (not inside async function)
// const result = await fetchUsername(); // ERROR! await is only valid inside async functions.

// Correct: wrap it in an async function
async function main(): Promise<void> {
  const result = await fetchUsername();
  console.log(result);
}

main(); // Call the async function to start execution.
```

---

## 4. Error Handling in Async Code

When a Promise rejects, `await` throws an error. You catch it with a standard `try/catch` block (covered in full in Module 11, but introduced here because async/await relies on it)
```typescript
async function loadUserData(userId: string): Promise<void> {
  try {
    const user = await fetchUserById(userId); // Might throw if user is not found.
    console.log("Loaded:", user.username);
  } catch (error) {
    // If the await above threw, execution jumps here.
    console.log("Failed to load user.");
  }
}
```

`try` contains the code you want to run. `catch` contains the code that runs if anything inside `try` throws an error. The error thrown by the rejected Promise is passed as the `catch` parameter.

---

## 5. Typing Async Functions

The return type of any async function is always `Promise<T>`. If your function has no return value, it is `Promise<void>`
```typescript
// Returns Promise<string>
async function getTitle(): Promise<string> {
  return "TypeScript Developer";
}

// Returns Promise<number>
async function getScore(): Promise<number> {
  return 95;
}

// Returns nothing meaningful
async function logStatus(): Promise<void> {
  console.log("System running.");
}
```

---

## 6. Fetching Data: A Real Example

Here is a realistic simulation of fetching data from an API, which is the most common use of async/await
```typescript
interface Post {
  id: number;
  title: string;
  body: string;
}

// Simulates a network request that takes time to complete
async function fetchPost(id: number): Promise<Post> {
  // In a real app, you would use
  // const response = await fetch(`https://api.example.com/posts/${id}`);
  // const data = await response.json();
  // return data;

  // Simulation
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve({ id, title: "TypeScript is Great", body: "Here is why..." });
    }, 500);
  });
}

async function displayPost(): Promise<void> {
  console.log("Fetching post...");
  const post = await fetchPost(1);
  console.log("Title:", post.title);
  console.log("Body:", post.body);
}

displayPost();
```

---

## 7. Running Multiple Async Tasks at the Same Time: `Promise.all`

If you have multiple async tasks that do not depend on each other, running them one at a time wastes time. `Promise.all` lets you start all of them simultaneously and wait for all of them to finish
```typescript
async function loadDashboard(): Promise<void> {
  // Without Promise.all - runs sequentially (wasteful)
  // const user   = await fetchUser(1);  // Wait 1 second
  // const orders = await fetchOrders(); // Then wait another 1 second (2 seconds total)

  // With Promise.all - runs in parallel (efficient)
  const [user, orders] = await Promise.all([
    fetchUser(1),    // Both start at the same time.
    fetchOrders()    // Total wait time = the slowest one, not the sum.
  ]);

  console.log("User:", user);
  console.log("Orders:", orders);
}
```

`Promise.all` takes an array of Promises and returns a single Promise that resolves when ALL of them have resolved. The result is an array of their resolved values in the same order.

If any one of the Promises rejects, `Promise.all` immediately rejects with that error.

---

## 8. `Promise.allSettled`: When You Want All Results Regardless of Errors

`Promise.allSettled` is like `Promise.all` but it never rejects. It waits for every Promise to either fulfill or reject and gives you the outcome for each one
```typescript
async function tryLoadAll(): Promise<void> {
  const results = await Promise.allSettled([
    fetchUser(1),
    fetchUser(999) // This one will fail (user 999 does not exist).
  ]);

  results.forEach((result) => {
    if (result.status === "fulfilled") {
      console.log("Success:", result.value);
    } else {
      console.log("Failed:", result.reason);
    }
  });
}
```

Use `Promise.allSettled` when you want to attempt multiple operations and handle successes and failures individually.

---

## 9. Async Functions in Classes

Class methods can also be async
```typescript
interface User {
  id: string;
  username: string;
}

class UserService {
  async findById(id: string): Promise<User | null> {
    // Simulate database lookup
    if (id === "1") {
      return { id: "1", username: "alice" };
    }
    return null;
  }

  async createUser(username: string): Promise<User> {
    const user: User = { id: Date.now().toString(), username };
    // In a real app: await db.insert(user);
    return user;
  }
}

async function main(): Promise<void> {
  const service = new UserService();
  const user = await service.findById("1");
  if (user !== null) {
    console.log("Found:", user.username);
  }
}

main();
```

---

## 10. Common Mistakes to Avoid

### Forgetting `await`

If you forget `await`, you get a Promise object instead of the resolved value. TypeScript will warn you about this in most cases
```typescript
async function badExample(): Promise<void> {
  const name = fetchUsername(); // Missing await! 'name' is Promise<string>, not string.
  console.log(name); // Outputs: Promise { <pending> }
}
```

### Using `await` in a Non-Async Function

`await` is only valid inside functions marked with `async`. Trying to use it elsewhere is a syntax error.

### Sequential `await` When Parallel Would Be Better

```typescript
// Slow (sequential)
const a = await taskA();
const b = await taskB(); // taskB only starts after taskA finishes.

// Fast (parallel)
const [a, b] = await Promise.all([taskA(), taskB()]); // Both start immediately.
```

If two tasks are independent, always prefer `Promise.all`.
