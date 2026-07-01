# Question 01 Answer

**How many responsibilities:**
Four: data fetching, access control, date formatting, and UI rendering.

**What belongs in the UI component:**
Only the rendering responsibility  -  taking data that has already been fetched, validated, and formatted, and displaying it as HTML/JSX. The component should be a pure display layer.

**Where the other responsibilities belong:**
- Data fetching belongs in a service or custom hook (e.g. `useUserData()`).
- Access control (authorization) belongs on the backend or in a dedicated auth utility.
- Date formatting belongs in a utility function (e.g. `formatDate()` in `utils/date.ts`).

**Why mixing is harmful:**
When a component does everything, it becomes impossible to test each concern independently. To test the date formatting logic you have to mount the entire component, mock network requests, and satisfy authentication. Changing any one concern requires modifying and re-testing the whole file. And when a bug appears, it is harder to isolate where it came from. Separation means you can test, replace, or modify each piece without touching the others.
