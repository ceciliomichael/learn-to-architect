# Exercise Solution: Custom Elements, Shadow DOM, and Web Component Boundaries

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

## Why this works

The reference keeps browser I/O, runtime validation, lifecycle ownership, and user recovery explicit. Adaptations are correct when they preserve those contracts and observable behavior.

