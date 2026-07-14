# Module 24 Exercises

Use this model:

```typescript
interface Product {
  id: string;
  name: string;
  price: number;
  description?: string;
  inStock: boolean;
}
```

## Exercise 1: Derive operation types

Create:

- `NewProduct` without `id`
- `ProductSummary` with only `id`, `name`, and `price`
- `ProductUpdate` where name, price, description, and inStock are optional but id is not present
- `ReadonlyProduct`

## Exercise 2: Closed labels

Create `type StockState = "available" | "low" | "empty"`. Use `Record` to require one display label for each state.

## Exercise 3: Build a mapped type

Write `Nullable<T>` that keeps every key but adds `null` to each value type.

## Exercise 4: Runtime summary

Write `toProductSummary(product: Product): ProductSummary`. Confirm that the returned object contains only the selected runtime properties.

## Exercise 5: Choose clarity

Compare a deeply nested utility expression with an explicit three-property interface. Explain when the explicit form would be easier for a public function contract.

## Completion checklist

- [ ] I used the common utility types.
- [ ] I built a closed `Record`.
- [ ] I wrote a simple mapped type.
- [ ] I separated static transformations from runtime values.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
