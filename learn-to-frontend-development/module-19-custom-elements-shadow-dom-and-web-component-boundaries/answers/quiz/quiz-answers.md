# Quiz Answers: Custom Elements, Shadow DOM, and Web Component Boundaries

1. **What must a custom-element name contain?**

   A hyphen, reserving it from built-in HTML names.

2. **When does connectedCallback run?**

   When the element is connected to a document.

3. **Why guard customElements.define?**

   Defining the same name twice throws.

4. **What does Shadow DOM provide?**

   An encapsulated tree and style boundary with deliberate slots and exposed parts.

5. **Should a custom element hide essential fallback content?**

   No. Design usable semantics and upgrade behavior.

