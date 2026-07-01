# Module 10 Quiz Answers

Detailed answers for Module 10 quiz.

---

### Answer 1:
Co-locating API calls directly inside UI components couples presentation logic tightly to backend infrastructure.  
Extracting data calls into dedicated `services/` separates responsibilities, allowing data fetching layers to be independently tested, mocked, cached, and reused across multiple UI components without duplicating logic.

---

### Answer 2:
Circular dependencies occur when modules directly or indirectly reference each other in a closed loop. During runtime initialization, one module may attempt to access exports from another before execution completes, resulting in `undefined` references and application crashes.

---

### Answer 3:
Exceeding 300 lines usually indicates that a file is acting as a monolithic "God Object" or utility dumping ground, managing multiple distinct responsibilities (orchestration, validation, data transformation, and state management) rather than adhering to the Single Responsibility Principle.
