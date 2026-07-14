# Quiz Answers: URLs, Search Parameters, History, and Navigation

1. **Why use URL and URLSearchParams?**

   They encode and parse URL components according to URL rules.

2. **What does pushState do?**

   It adds a same-origin history entry without navigating by itself.

3. **What event responds to history traversal?**

   popstate.

4. **Should every keystroke create a history entry?**

   Usually no; replaceState or delayed commits may better represent meaningful navigation.

5. **Can pushState change to another origin?**

   No. The new URL must remain same-origin.

