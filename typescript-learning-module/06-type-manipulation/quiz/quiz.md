# Module 06 Quiz: Type Manipulation & Utility Types

Write your answers inside the **ANSWER HERE** blocks below.

---

### Question 1: `keyof` Operator
Given:
```typescript
interface Settings {
  volume: number;
  muted: boolean;
}
type SettingsKeys = keyof Settings;
```
What is the exact resolved type of `SettingsKeys`?

A) `string`  
B) `"volume" | "muted"`  
C) `number | boolean`  
D) `["volume", "muted"]`

#### ✍️ ANSWER HERE:
> Choice: 
> Explanation: 

---

### Question 2: `typeof` in Type Context vs Runtime Context
In JavaScript, writing `typeof 42` returns the runtime string `"number"`. When you write `type T = typeof myVariable;` in TypeScript, does `typeof` execute at runtime? Explain what happens during compilation.

#### ✍️ ANSWER HERE:
> Does it execute at runtime? 
> Explanation: 

---

### Question 3: `Record<K, T>` Utility Type
Which of the following is equivalent to `Record<"admin" | "guest", number>`?

A) `[number, number]`  
B) `{ admin?: number; guest?: number }`  
C) `{ admin: number; guest: number }`  
D) `{ key: "admin" | "guest"; value: number }`

#### ✍️ ANSWER HERE:
> Choice: 
> Explanation: 

---

### Question 4: Indexed Access Types
If you have `interface Person { address: { street: string; zip: number } }`, what syntax do you use to extract the type of `address` into a new type alias?

A) `type Address = Person.address;`  
B) `type Address = Person["address"];`  
C) `type Address = Pick<Person, address>;`  
D) `type Address = typeof Person.address;`

#### ✍️ ANSWER HERE:
> Choice: 
> Explanation: 
