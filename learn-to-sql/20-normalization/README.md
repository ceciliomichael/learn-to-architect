# Module 20: Design Relational Data and Normalize It

## What you will learn

You will separate facts by meaning, reduce update problems, and apply first through third normal form in practical language.

## Begin with entities and relationships

An entity is a kind of thing the database tracks, such as product, category, order, or customer. An attribute is one fact about it. A relationship connects entities.

Good design asks where each fact belongs and what key determines it.

## Recognize update problems

Imagine one table:

```text
order_id | customer_email | product_1 | product_2 | product_3
```

Problems include:

- A fixed number of product columns
- Empty columns for smaller orders
- Hard searches across repeated column roles
- No ordinary foreign key from each product cell

An orders table plus one order-items row per product relationship avoids these problems.

## First normal form

For practical course purposes, first normal form means each row-column position holds one value from the column's domain, each row is identifiable, and repeating groups become rows rather than numbered columns or comma-separated lists.

## Second normal form

When a table has a composite key, every nonkey fact should depend on the whole key.

In `order_items(order_id, product_id, quantity, unit_price_cents)`, quantity depends on both order and product. Product name depends only on product, so it belongs in `products`, not repeated in every order item.

## Third normal form

Nonkey facts should not depend on other nonkey facts.

If a product row stores both `category_id` and `category_name`, the name depends on category identity, not directly on product identity. Store it once in `categories` and join it when needed.

## Functional dependency in plain language

`A -> B` means one allowed value of A determines one value of B. A primary key determines the facts of its row. Business rules, not sample data, establish the dependency.

Two current rows sharing a value do not prove a permanent rule.

## Normalization is not table splitting by instinct

Every split should protect a real fact and preserve valid relationships. Too many tables without clear entities create unnecessary joins and confusion.

Sometimes a measured production workload stores a derived or repeated value for performance. That is controlled denormalization. It needs:

- A documented source of truth
- A reliable synchronization rule
- Measured evidence of benefit
- Tests for inconsistency

Normalize for correctness first. Denormalize only from evidence.

## A design review checklist

1. What does one row represent?
2. What key identifies it?
3. Does each column describe that row's entity or relationship?
4. Are lists stored as rows instead of packed text?
5. Can constraints protect the relationships?
6. Which fact is the source of truth?

## Common mistakes

### Treating normal forms as table-count goals

They are dependency rules, not a contest to create more tables.

### Storing calculated totals without a policy

They can disagree with line items. Calculate them or define synchronization carefully.

### Designing from one sample dataset

Use business rules and possible future valid states, not coincidences in six rows.

## Check your understanding

You are ready when you can state one row's meaning, identify which key determines each fact, and explain a justified table split.
