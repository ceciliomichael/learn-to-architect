# Module 10: Asynchronous Programming

In every module up until now, our code executed **Synchronously**: the computer ran line 1, finished line 1, moved to line 2, finished line 2, and proceeded sequentially down the page. 

But real-world software must communicate with the outside world. When your application queries a database across the network, downloads an image from a cloud bucket, or fetches user data from a REST API, that network request takes time—hundreds of milliseconds or even seconds!

If your program stopped and froze completely while waiting for a network request to finish, your user interface would lock up; users wouldn't be able to click buttons or scroll the page. 

This module teaches you how to master **Asynchronous Programming** in TypeScript. We will explore how to model future data using **`Promise<T>`**, how to write clean, linear asynchronous code using **`async` / `await`**, how to handle network failures gracefully using `try / catch` blocks, and how to execute multiple network operations in parallel using `Promise.all`.

---

## 1. Synchronous vs. Asynchronous Execution

### Let's Take a Restaurant Kitchen as an Example
To understand how asynchronous execution works without getting lost in computer science terminology, imagine a busy restaurant kitchen with a single chef.
* **The Synchronous Chef (Blocking Execution):** A waiter hands the chef an order for a baked lasagna (which takes 30 minutes in the oven). The chef puts the lasagna in the oven, folds their arms, and stands completely frozen in front of the oven door staring at it for 30 solid minutes! While standing there frozen, the chef refuses to chop salads, toast bread, or cook soup for any other customers. The entire restaurant grinds to a halt. This is **Synchronous Blocking**.
* **The Asynchronous Chef (Non-Blocking Event Loop):** The chef puts the lasagna into the oven and sets an automated kitchen timer. *Instead of standing frozen in front of the oven*, the chef immediately turns around and begins chopping salad, grilling steaks, and plating appetizers for other tables! When the oven timer eventually rings 30 minutes later, the chef finishes plating their current dish, walks over, and pulls the cooked lasagna out of the oven. This is **Asynchronous Non-Blocking Execution**.

In JavaScript and TypeScript, your code runs on a **Single Thread** (one chef). To prevent the thread from freezing during slow network requests or timer delays, TypeScript uses an asynchronous event loop: it fires off the network request, sets an internal notification timer, and continues executing other code until the network response arrives!

---

## 2. What is a Promise (`Promise<T>`)?

### Think of an Automated Restaurant Buzzer Pager
When you walk into a crowded, popular restaurant without a reservation, the host cannot seat you immediately. Instead, they hand you a flashing electronic pager buzzer and say: *"Your table isn't ready yet, but this buzzer is our **Promise** to seat you when a table opens up."*

While holding that buzzer, you are free to sit at the bar, chat with friends, or read a book. The pager buzzer can transition into three distinct states:
1. **Pending:** The pager is sitting quietly in your hand while you wait. The outcome is undecided.
2. **Fulfilled (Resolved):** The pager flashes green and vibrates! The host leads you to your table and hands you your menu (`the data payload`).
3. **Rejected:** The host walks over, apologizes, and tells you the kitchen experienced a fire and the restaurant must close. Your reservation is cancelled (`an error payload`).

In TypeScript, a **`Promise<T>`** is the digital equivalent of that restaurant buzzer! It is a placeholder object representing an asynchronous operation that hasn't completed yet, but promises to eventually yield a data value of type **`T`** (or throw an error).

### Declaring and Constructing Promises
When a function performs an asynchronous action, you annotate its return type as `Promise<DataType>`:

```typescript
// A function returning a Promise that will eventually resolve to a text string!
function simulateNetworkDelay(): Promise<string> {
  // We construct a new Promise object, passing a callback with resolve and reject tools
  return new Promise<string>((resolve, reject) => {
    console.log("Network request initiated...");

    // We use setTimeout to simulate a 2-second (2000 millisecond) network delay
    setTimeout(() => {
      const isNetworkOnline: boolean = true;

      if (isNetworkOnline) {
        // We resolve the promise, handing back our data payload!
        resolve("Server response: Data downloaded successfully!");
      } else {
        // We reject the promise, reporting a failure!
        reject(new Error("Network Error: Connection timed out."));
      }
    }, 2000);
  });
}
```

### Syntax Symbols vs. Promise Names
| Word in Example | What It Is | Why It Matters |
| :--- | :--- | :--- |
| `Promise<T>` | **Built-in Generic Class** | Standard language class representing an eventual asynchronous outcome. |
| `resolve`, `reject` | **Built-in Callback Tools** | Functions provided by the runtime engine to signal success or failure. |
| `simulateNetworkDelay` | **Your Custom Function Label** | The name of the action engine generating the promise. |

---

## 3. The Modern Standard: `async` and `await`

### Picture Answering a Walkie-Talkie
Before the modern `async`/`await` syntax was introduced in 2017, developers handled promises by chaining `.then()` and `.catch()` callback methods together. In complex engineering projects, chaining dozens of `.then()` callbacks inside one another created a notoriously unreadable pyramid of indented code known as **Callback Hell**.

To eliminate callback hell, TypeScript provides two keywords that let you write asynchronous code that *reads* just like clean, top-to-bottom synchronous code: **`async`** and **`await`**.

### How `async` and `await` Operate
1. **The `async` Keyword:** Placing `async` in front of a function declaration tells TypeScript: *"This function performs asynchronous work. **Automatically wrap whatever value this function returns inside a `Promise<T>`!**"*
2. **The `await` Keyword:** You can **only use `await` inside an `async` function!** Placing `await` in front of a Promise tells TypeScript: *"Pause execution of this specific function right here! Wait until the buzzer pager resolves, unpack the data payload from inside the Promise container, and return the raw value so we can store it in a normal variable!"*

```typescript
// 1. We mark the function as async, returning a Promise<void>
async function executeDataFetch(): Promise<void> {
  console.log("[STEP 1]: Initiating fetch sequence...");

  // 2. We use 'await' to pause the function until simulateNetworkDelay() resolves!
  // Notice that 'await' automatically unpacks the string out of the Promise<string> container!
  const serverMessage: string = await simulateNetworkDelay();

  console.log(`[STEP 2]: Received payload -> ${serverMessage}`);
  console.log("[STEP 3]: Processing complete!");
}

// When we call executeDataFetch(), it runs asynchronously!
executeDataFetch();
console.log("[STEP 0]: This prints immediately while the network request is still pending!");
```

### Deconstructing Async/Await Syntax
Let's look at `const serverMessage: string = await simulateNetworkDelay();`:

* `const` -> Permanent variable declaration.
* `serverMessage` -> Developer name for the container storing the unpacked data.
* `:` -> Type annotation anchor.
* `string` -> The raw primitive data type we expect *after* the Promise container is unpacked.
* `=` -> Assignment operator.
* `await` -> The asynchronous pause keyword! This instructs the JavaScript event loop: *"Suspend this function's execution until the Promise on the right fulfills, then extract its contents."*
* `simulateNetworkDelay()` -> Our function executing the asynchronous operation and returning a `Promise<string>`.
* `;` -> Statement terminator.

### Why Why This Matters in Real-World Projects
In full-stack web applications, rendering a user dashboard requires executing sequential database lookups: first you must query the database for the user's authentication token, then you use that token to query their billing profile, and finally you use their billing profile to query their recent invoices.

Attempting to coordinate three sequential network requests using old-school callbacks creates messy, unmaintainable code. Using `async`/`await` allows senior architects to write sequential network pipelines that read like a simple, elegant book:

```typescript
async function loadUserDashboard(userId: string): Promise<DashboardData> {
  // Step 1: Wait for auth profile
  const authProfile = await fetchAuthProfile(userId);
  
  // Step 2: Use auth token to wait for billing info
  const billingInfo = await fetchBillingInfo(authProfile.token);
  
  // Step 3: Use billing ID to wait for invoices
  const invoices = await fetchInvoices(billingInfo.accountId);
  
  return { profile: authProfile, billing: billingInfo, invoices: invoices };
}
```

---

## 4. Error Handling in Asynchronous Code (`try / catch / finally`)

### Imagine an In-Flight Airplane Emergency Landing Protocol
When an airplane is flying smoothly at cruising altitude, the pilots operate under normal flight procedures (`the try block`). However, aviation engineers know that engines can encounter turbulence or mechanical glitches at any moment.

To prepare for failures, pilots have an emergency landing protocol (`the catch block`). If an engine malfunctions during flight, the pilots immediately abort normal procedures and execute the emergency checklist to land the plane safely. 

Regardless of whether the flight landed normally or executed an emergency landing, when the plane reaches the terminal, the ground crew *always* performs standard post-flight maintenance (`the finally block`).

In TypeScript, you wrap asynchronous network calls inside **`try / catch / finally`** blocks to prevent network timeouts or server crashes from bringing down your entire application!

### Building Crash-Proof Network Handlers
When an `await` promise rejects (fails), it throws an exception. If you don't catch that exception, your program crashes! Here is the industry-standard pattern for handling async errors:

```typescript
async function fetchUserProfileSafe(userId: string): Promise<void> {
  // 1. The TRY block: We attempt our normal, happy-path operations here
  try {
    console.log(`[TRY]: Requesting profile for user ${userId}...`);
    const responseMessage: string = await simulateNetworkDelay();
    console.log(`[TRY]: Success! ${responseMessage}`);
  } 
  // 2. The CATCH block: If ANY promise rejects above, execution jumps instantly here!
  catch (error: unknown) {
    // Notice: in TypeScript, caught errors are typed as 'unknown' by default!
    // We must use type narrowing to inspect the error safely:
    if (error instanceof Error) {
      console.error(`[CATCH]: Network request failed! Reason: ${error.message}`);
    } else {
      console.error("[CATCH]: An unknown error occurred.", error);
    }
  } 
  // 3. The FINALLY block: Executes 100% of the time, regardless of success or failure!
  // Perfect for hiding UI loading spinners or closing database connections.
  finally {
    console.log("[FINALLY]: Cleaning up network resources and stopping UI loading spinner.");
  }
}
```

### Why Caught Errors Are Typed as `unknown`
Why does TypeScript type `catch (error: unknown)` instead of `catch (error: Error)`?
Because in JavaScript, developers are legally allowed to throw *anything*! A third-party library might throw a standard Error object (`throw new Error("fail")`), but poorly written legacy code might throw a text string (`throw "Server down!"`), or even a number (`throw 404`). 

Because TypeScript cannot predict what data type an external API might throw across the network, it enforces strict safety by typing caught exceptions as `unknown`, compelling you to check `if (error instanceof Error)` before accessing `.message`!

---

## 5. Typing REST API Requests (`fetch` and JSON Parsing)

### Think of Customs Border Inspection for Imported Cargo
When a cargo ship docks at a port, it unloads metal shipping crates containing goods purchased from a foreign country (`a REST API response`). The port customs officers do not simply trust whatever label is printed on the outside of the crate! They open the crate, inspect the cargo, and verify that the contents conform strictly to legal safety standards before releasing the goods into the domestic market.

In TypeScript, when you use the browser's built-in **`fetch()`** function to download JSON data from an external REST API, **`response.json()` returns `Promise<any>` by default!** 

If you don't inspect that incoming data, a corrupted server response can silently infiltrate your codebase. Let's see how senior architects type and verify network API requests!

### Fetching and Typing Remote Data
To fetch data safely over HTTP, we define an interface blueprint representing our expected JSON schema, and use type assertions or validation functions after downloading:

```typescript
// 1. Define our expected JSON schema blueprint
interface RemoteTodoItem {
  userId: number;
  id: number;
  title: string;
  completed: boolean;
}

// 2. Write an async fetcher function returning a typed Promise
async function fetchTodoItem(todoId: number): Promise<RemoteTodoItem> {
  const url: string = `https://jsonplaceholder.typicode.com/todos/${todoId}`;
  
  // Await the network HTTP connection
  const response: Response = await fetch(url);

  // Always verify that the HTTP status code is 200 OK before parsing!
  if (!response.ok) {
    throw new Error(`HTTP Request failed with status: ${response.status}`);
  }

  // Await the JSON stream parsing. Notice we cast the raw result to our blueprint!
  const rawData: unknown = await response.json();

  // In production, we perform basic runtime verification before casting:
  if (typeof rawData === "object" && rawData !== null && "title" in rawData) {
    return rawData as RemoteTodoItem;
  } else {
    throw new Error("API Response schema mismatch: Missing required properties!");
  }
}

// Executing our typed API fetcher!
async function displayTodo() {
  try {
    const todo: RemoteTodoItem = await fetchTodoItem(1);
    console.log(`Todo #${todo.id}: "${todo.title}" | Completed: ${todo.completed}`);
  } catch (err) {
    console.error("Failed to load todo:", err);
  }
}
```

---

## 6. Parallel Asynchronous Execution (`Promise.all`)

### Picture Sending Three Assistants to Three Different Stores
Imagine you are planning a massive corporate banquet. You need to purchase three things: a custom wedding cake from a bakery across town, 500 steaks from a wholesale butcher, and 50 tables from a furniture warehouse.
* **The Slow Sequential Approach:** You drive across town to the bakery, wait an hour for the cake, drive back. Then you drive to the butcher, wait an hour for the steaks, drive back. Then you drive to the warehouse, wait an hour for tables. The total time taken is **3 solid hours**.
* **The Fast Parallel Approach (`Promise.all`):** You hire three assistants! At 9:00 AM, you send Assistant A to the bakery, Assistant B to the butcher, and Assistant C to the warehouse *at the exact same time*. All three assistants do their errands concurrently. At 10:00 AM, all three assistants return to your office simultaneously! The total time taken is **only 1 hour**!

In TypeScript, when you have multiple independent network requests that don't depend on each other's data, executing them sequentially using sequential `await` statements wastes enormous amounts of time. You should execute them concurrently using **`Promise.all([...])`**!

### Executing Concurrent Operations
`Promise.all` accepts an array of Promise objects, executes all of them simultaneously across the event loop, and returns a single Promise resolving to a **Tuple array** containing all unpacked results in their exact original order:

```typescript
async function fetchDashboardMetricsParallel(): Promise<void> {
  console.time("ParallelFetchTime");
  console.log("Initiating concurrent network requests...");

  // We fire off three independent async operations simultaneously!
  const userPromise: Promise<string> = simulateNetworkDelay(); // Takes 2 sec
  const salesPromise: Promise<string> = simulateNetworkDelay(); // Takes 2 sec
  const inventoryPromise: Promise<string> = simulateNetworkDelay(); // Takes 2 sec

  // We use Promise.all to await all three simultaneously!
  // TypeScript correctly types the result as a tuple: [string, string, string]
  const [userResult, salesResult, inventoryResult] = await Promise.all([
    userPromise,
    salesPromise,
    inventoryPromise
  ]);

  console.log("All concurrent requests completed!");
  console.log(`User Data: ${userResult}`);
  console.log(`Sales Data: ${salesResult}`);
  console.log(`Inventory Data: ${inventoryResult}`);
  
  // Total execution time will be ~2 seconds instead of 6 seconds!
  console.timeEnd("ParallelFetchTime");
}
```

#### What about `Promise.allSettled` and `Promise.race`?
* **`Promise.all` (All-or-Nothing):** If even *one* promise in the array rejects, the entire `Promise.all` immediately aborts and throws an error!
* **`Promise.allSettled` (Forgiving Concurrency):** Waits for all promises to finish, regardless of whether they succeeded or failed. It returns an array of status objects (`{ status: "fulfilled", value: ... }` or `{ status: "rejected", reason: ... }`). Perfect for rendering dashboards where one failed widget shouldn't crash the whole page!
* **`Promise.race` (The Fastest Winner):** Executes multiple promises simultaneously and returns strictly the result of *whichever promise finishes first!* Perfect for building network timeout race conditions (`Promise.race([fetchData(), startTimeoutTimer(5000)])`).

---

## 7. Real-World Use Cases and Common Pitfalls

### Summary of Critical Beginner Pitfalls to Remember
1. **The Forgetting `await` Trap:** What happens if you write `const data = fetchUser(1);` without the `await` keyword?
   `data` will not be your user object! It will be the **sealed `Promise<User>` container object itself**! If you try to access `data.username`, TypeScript will throw an error (`Property 'username' does not exist on type 'Promise<User>'`). Always check your types: if a variable says `Promise<...>`, you forgot to `await` it!
2. **The Sequential Waterfall Trap in Loops:** Beginners frequently write `for...of` loops that await network requests inside the loop:
   ```typescript
   // Slow Sequential Waterfall (Terrible Performance!):
   for (let id of userIds) {
     const user = await fetchUser(id); // Waits for user 1 to finish before starting user 2!
   }

   // Fast Concurrent Pipeline (Professional Architecture!):
   const userPromises = userIds.map(id => fetchUser(id)); // Fire all instantly!
   const allUsers = await Promise.all(userPromises);      // Await all concurrently!
   ```
3. **The Silent Floating Promise Trap:** If you call an async function inside a standard synchronous function (like a React button click handler or a DOM event listener), but you don't attach a `.catch()` or wrap it in a try/catch, any network failure will cause an **Unhandled Promise Rejection** warning in production logs! Senior architects ensure every async execution chain terminates with error handling.
