# Challenge 03: Custom Type Guard

Write a custom type guard to safely narrow between two user types.

## Your Tasks

1. Define two interfaces
   - `PremiumUser`: `{ plan: "premium"; monthlyFee: number; maxDownloads: number }`
   - `FreeUser`: `{ plan: "free"; dailyLimit: number }`

2. Write a custom type guard function `isPremiumUser(user: PremiumUser | FreeUser): user is PremiumUser`. Since both types already have a `plan` literal property, use `user.plan === "premium"` as the check inside the function body.

3. Write a function `printUserInfo(user: PremiumUser | FreeUser): void` that
   - Uses `isPremiumUser` to narrow the type.
   - If premium: logs `"Premium user. Fee: $[monthlyFee]/mo. Max downloads: [maxDownloads]"`.
   - If free: logs `"Free user. Daily limit: [dailyLimit] requests"`.

4. Create one `PremiumUser` object and one `FreeUser` object and test both.

## ANSWER HERE

```typescript
// Write your interfaces, type guard, and printUserInfo here
```
