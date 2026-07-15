# Quiz Answers: The DOM Tree and Safe Element Queries

1. **What does the DOM represent?**

   The browser's current parsed document tree, which may differ from the original source after parsing or updates.

2. **Why can querySelector return null?**

   No element may match at the time and root being queried.

3. **Why check instanceof?**

   A matching selector does not by itself prove the concrete element API expected by the code.

4. **When is getElementById useful?**

   When querying a document for one known id and handling its HTMLElement or null result.

5. **Why avoid a broad type assertion?**

   It suppresses evidence without checking runtime identity.

