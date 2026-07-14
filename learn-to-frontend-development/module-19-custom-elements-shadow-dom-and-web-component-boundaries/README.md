# Module 19: Custom Elements, Shadow DOM, and Web Component Boundaries

## What you will learn

Create a small custom element with lifecycle and attribute contracts without hiding ordinary HTML alternatives.

## Contracts to understand

- A hyphen, reserving it from built-in HTML names.
- When the element is connected to a document.
- Defining the same name twice throws.
- An encapsulated tree and style boundary with deliberate slots and exposed parts.
- No. Design usable semantics and upgrade behavior.

## Complete TypeScript example

```ts
class GardenNotice extends HTMLElement {
  static observedAttributes = ["message"];

  connectedCallback(): void {
    this.render();
  }

  attributeChangedCallback(): void {
    this.render();
  }

  private render(): void {
    this.textContent = this.getAttribute("message") ?? "Garden notice";
  }
}

if (!customElements.get("garden-notice")) {
  customElements.define("garden-notice", GardenNotice);
}
```

Type-check with strict DOM settings, run in the course browser project, and inspect the relevant developer-tool panel. Do not use a type assertion to replace missing runtime evidence.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 20](../module-20-unit-testing-browser-logic/README.md).

