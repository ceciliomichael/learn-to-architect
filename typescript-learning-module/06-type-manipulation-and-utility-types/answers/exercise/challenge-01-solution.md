# Challenge 01: Solution

```typescript
interface User {
  id: string;
  username: string;
  email: string;
  passwordHash: string;
  createdAt: Date;
}

// 1. All fields optional, id and createdAt removed
type UserUpdatePayload = Partial<Omit<User, "id" | "createdAt">>;

// 2. Only id, username, email
type PublicUser = Pick<User, "id" | "username" | "email">;

// 3. All fields readonly
type ImmutableUser = Readonly<User>;

// 4. Remove id and createdAt, keep everything else required
type NewUserInput = Omit<User, "id" | "createdAt">;

// Example objects
const update: UserUpdatePayload = { email: "newemail@example.com" };
console.log(update.email); // "newemail@example.com"

const profile: PublicUser = { id: "user-1", username: "alice", email: "alice@example.com" };
console.log(profile.username); // "alice"

const immutable: ImmutableUser = {
  id: "user-1", username: "alice", email: "a@a.com", passwordHash: "xyz", createdAt: new Date()
};
// immutable.username = "bob"; // ERROR: Cannot assign to 'username' because it is read-only.

const newUser: NewUserInput = {
  username: "nova",
  email: "nova@example.com",
  passwordHash: "hashedvalue"
};
console.log(newUser.username); // "nova"
```
