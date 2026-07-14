# Quiz Answers: Service Workers, Offline Behavior, and Update Safety

1. **What can a service worker intercept?**

   Requests within its controlled scope after activation and control.

2. **Why is offline-first not automatic?**

   Data freshness, mutations, authentication, cache limits, and conflict behavior need product rules.

3. **What is cache versioning for?**

   It separates deployments and enables removal or migration of stale assets.

4. **Should error responses be cached blindly?**

   No. Cache policy must inspect request and response suitability.

5. **Why test updates with two tabs?**

   An older worker may control existing clients while a new worker waits or activates.

