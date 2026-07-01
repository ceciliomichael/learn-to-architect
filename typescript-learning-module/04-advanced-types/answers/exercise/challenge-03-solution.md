# Challenge 03: Solution

```typescript
interface PremiumUser {
  plan: "premium";
  monthlyFee: number;
  maxDownloads: number;
}

interface FreeUser {
  plan: "free";
  dailyLimit: number;
}

function isPremiumUser(user: PremiumUser | FreeUser): user is PremiumUser {
  return user.plan === "premium";
}

function printUserInfo(user: PremiumUser | FreeUser): void {
  if (isPremiumUser(user)) {
    // TypeScript narrows 'user' to PremiumUser here:
    console.log(`Premium user. Fee: $${user.monthlyFee}/mo. Max downloads: ${user.maxDownloads}`);
  } else {
    // TypeScript narrows 'user' to FreeUser here:
    console.log(`Free user. Daily limit: ${user.dailyLimit} requests`);
  }
}

const premium: PremiumUser = { plan: "premium", monthlyFee: 9.99, maxDownloads: 100 };
const free: FreeUser        = { plan: "free",    dailyLimit: 10 };

printUserInfo(premium); // "Premium user. Fee: $9.99/mo. Max downloads: 100"
printUserInfo(free);    // "Free user. Daily limit: 10 requests"
```
