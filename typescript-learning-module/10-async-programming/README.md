# Module 10: Async Programming - Promises and Async/Await

In all previous modules, our code ran instantaneously. You asked for `1 + 1`, and the computer gave you `2` in the same millisecond. 

But real-world engineering is slow. When you ask a PostgreSQL database for 5,000 user records, or when you ask Stripe to process a credit card, it might take 3 full seconds. If you don't handle this delay correctly, your entire application will freeze, unable to click buttons or load animations.

This module introduces **Asynchronous Programming**: the art of telling your code to wait for slow tasks without freezing the rest of your application.

---

## 1. The Problem: Why Async Exists

### The Real-World Analogy: The Restaurant Kitchen
Imagine you are the only chef in a restaurant. A customer orders a baked potato (takes 45 minutes).
* **Synchronous (Blocking) Approach:** You put the potato in the oven, and then you stand in front of the oven staring at it for 45 minutes. You ignore all other customers. You cook nothing else. This is a disaster.
* **Asynchronous (Non-Blocking) Approach:** You put the potato in the oven and set a timer. While it bakes, you turn around and start making salads and pouring drinks for other customers. When the timer dings, you go back and take the potato out.

### The Core Technical Concept
JavaScript is single-threaded (one chef). If you write a piece of code that takes 3 seconds to execute, the entire web browser freezes for 3 seconds. The user cannot scroll, click, or type. This is called **Blocking**.

**Asynchronous programming** allows your code to say: *"Start this slow network request. Go do other things. Notify me when the request finishes."*

---

## 2. What is a Promise?

### The Real-World Analogy: The Coffee Shop Pager
When you order a latte at a busy coffee shop, the barista doesn't hand you a coffee immediately. They hand you a little plastic **Pager** that flashes red. 
You walk away and sit down. The pager represents a *future* coffee.
- Right now, the pager is **Pending** (coffee is being made).
- Eventually, the pager buzzes! It is **Fulfilled** (you exchange the pager for your coffee).
- Or, the barista shouts that they are out of milk. It is **Rejected** (you get an error).

### The Core Technical Concept
A `Promise` is the digital version of that plastic pager. It is an object that represents the eventual completion (or failure) of an asynchronous operation.

When you type a function that returns a Promise, you must tell TypeScript exactly what type of data the Promise will eventually spit out. You do this using Generics (`Promise<T>`).

```typescript
// The function returns a Pager that promises to eventually deliver a string!
function fetchUsername(): Promise<string> {
  return new Promise((resolve, reject) => {
    // Simulating a slow 2-second database lookup...
    setTimeout(() => {
      resolve("Alice"); // The pager buzzes! We deliver the string!
    }, 2000);
  });
}
```

### Handling the Pager (`.then` and `.catch`)
To receive the data when the Promise finishes, you chain `.then()` and `.catch()` callbacks onto it:

```typescript
fetchUsername()
  .then((name) => {
    // This block ONLY runs when the Promise is Fulfilled!
    console.log("Success! The name is: " + name);
  })
  .catch((error) => {
    // This block ONLY runs if the Promise is Rejected!
    console.log("Database crashed: " + error);
  });
```

---

## 3. `async` and `await`: The Clean Way

Chaining `.then()` works, but if you need to fetch a user, *then* fetch their orders, *then* fetch their shipping address, you end up with massive, deeply nested "Pyramids of Doom" that are impossible to read.

Modern TypeScript solves this using `async` and `await`.

### The Core Technical Concept
* **`async`**: A keyword you put in front of a function. It forces the function to return a `Promise`.
* **`await`**: A keyword you put inside an `async` function. It pauses the exact line of code it is on until the Promise finishes, without freezing the rest of the application!

```typescript
// We mark the function as async so we are allowed to use await!
async function displayUser(): Promise<void> {
  console.log("1. Starting lookup...");

  // The code PAUSES right here for 2 seconds. 
  // It waits for the Promise to finish, and extracts the string into 'name'!
  const name = await fetchUsername(); 

  console.log("2. Finished! Name is: " + name);
}
```

**CRITICAL RULE:** You can ONLY use the `await` keyword inside a function that has the `async` keyword! 

---

## 4. Error Handling in Async Code

When you use `.then()`, you use `.catch()` to handle errors. 
When you use `await`, you must use a traditional `try / catch` block to handle errors.

```typescript
async function safeLoadData(): Promise<void> {
  try {
    // The code INSIDE the 'try' block is executed.
    const user = await fetchUsername(); 
    console.log("Got user: " + user);
  } catch (error) {
    // If the await above fails (Promise is Rejected), execution instantly JUMPS here!
    console.log("Something went wrong! Fallback to default.");
  }
}
```

### Why Senior Developers Require This
If an API request times out and you don't have a `try/catch` block, the `await` keyword will throw an "Unhandled Promise Rejection". In modern Node.js, this will literally crash your entire server and take your website offline for all users!

---

## 5. Typing Async Functions

### The Core Technical Concept
If a function is marked as `async`, **it must always return a Promise type**, even if you just return a plain string inside the body! TypeScript will automatically wrap your plain string in a Promise invisibly.

```typescript
// BAD: 
// async function getAge(): number { return 25; } 
// COMPILER ERROR: The return type of an async function must be the global Promise<T>.

// GOOD:
async function getAge(): Promise<number> { 
  return 25; 
}

// If the function returns nothing, use Promise<void>
async function logAudit(): Promise<void> {
  console.log("Audited.");
}
```

---

## 6. Running Multiple Async Tasks at the Same Time: `Promise.all`

### The Real-World Analogy: The Laundry Machine
You need to wash clothes (takes 30 mins) and dry dishes (takes 30 mins).
If you do them sequentially, it takes 60 minutes.
If you do them in parallel (turn on both machines at the exact same time), it takes 30 minutes!

### The Core Technical Concept
If you have multiple `await` calls that don't rely on each other, putting them on separate lines is horribly inefficient. `Promise.all` allows you to fire them all off simultaneously.

```typescript
async function fetchUser(id: string): Promise<string> { /* ... */ }
async function fetchOrders(id: string): Promise<number[]> { /* ... */ }

async function loadDashboardSequentially() {
  // SLOW! Waits 2 seconds, then waits ANOTHER 2 seconds (4s total)
  const user = await fetchUser("1");
  const orders = await fetchOrders("1"); 
}

async function loadDashboardParallel() {
  // FAST! Fires both at the exact same time! (2s total)
  // We use an array destructuring pattern to catch both results!
  const [user, orders] = await Promise.all([
    fetchUser("1"),
    fetchOrders("1")
  ]);
}
```

**Warning:** If *any single one* of the Promises inside `Promise.all` fails, the entire `Promise.all` immediately crashes and throws an error!

---

## 7. `Promise.allSettled`: When You Want All Results Regardless of Errors

### The Core Technical Concept
If you are sending promotional emails to 5,000 users at once, you don't want the entire batch to fail just because User #42 has a typo in their email address.

`Promise.allSettled` runs everything in parallel like `Promise.all`, but **it never throws an error!** Instead, it waits for every single task to finish, and gives you a detailed report of which ones succeeded and which ones failed.

```typescript
async function sendMassEmails() {
  const reports = await Promise.allSettled([
    sendEmail("alice@a.com"),
    sendEmail("bob@b.com"),     // Imagine this one fails
    sendEmail("charlie@c.com")
  ]);

  // Reports is an array detailing the exact outcome of every email!
  reports.forEach(report => {
    if (report.status === "fulfilled") {
      console.log("Success! Value: ", report.value);
    } else {
      console.log("Failed! Reason: ", report.reason);
    }
  });
}
```

---

## 8. Real-World Use Cases and Common Pitfalls

### Summary of Critical Beginner Pitfalls to Remember
1. **Forgetting `await`:** If you write `const user = fetchUsername();` (without `await`), `user` is NOT a string! It is literally a pending plastic Pager object (`Promise<string>`). If you try to run `user.toUpperCase()`, the application will crash. Always remember your `await` keywords!
2. **Sequential `await` Abuse:** Beginners often write a chain of 10 `await` statements in a row. If they are independent database queries, you are making your user wait 10x longer than necessary. Always use `Promise.all` when queries do not depend on each other's results!
3. **Missing `try / catch`:** In modern React or Node.js apps, wrapping your network requests in `try/catch` is non-negotiable. If you don't, a blip in the user's WiFi connection will cause an unhandled rejection that completely breaks the user interface!
