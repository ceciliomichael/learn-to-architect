# Quiz Answers: Fetch, HTTP Results, Headers, and Content Types

1. **Does fetch reject for HTTP 404?**

   No. It normally resolves with a Response; code checks status.

2. **What does response.ok mean?**

   The status is in the 200 through 299 range.

3. **Why check Content-Type?**

   Status alone does not prove the body representation matches the expected decoder.

4. **What type should unvalidated JSON have?**

   unknown.

5. **Why encode a path value?**

   Untrusted text must not accidentally change URL path structure.

