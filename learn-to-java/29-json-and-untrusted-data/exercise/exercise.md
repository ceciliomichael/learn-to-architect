# Exercise: JSON and Untrusted Data

1. Recreate the example in a disposable project using the documented source layout.
2. Run or verify it with mvn test or mvn exec:java with tools.jackson.core:jackson-databind:3.1.3.
3. Confirm this behavior: Product[name=Pen, priceCents=125].
4. Reject blank names, negative prices, extra fields, oversized input, and trailing JSON values.
5. Explain how every listed contract is enforced and what would break if it were removed.

Do not commit generated caches, downloaded libraries, credentials, or real user data.

