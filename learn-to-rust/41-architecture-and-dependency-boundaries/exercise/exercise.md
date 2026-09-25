# Exercises: Module 41

## 1. Trace dependency direction

Given:

~~~text
main
 |
 v
HTTP adapter
 |
 v
pricing domain
~~~

Answer:

1. Should pricing domain need reqwest types?
2. Which layer should translate an HTTP payload into validated pricing inputs?
3. Where should the concrete HTTP client normally be constructed?

## 2. Repair mixed responsibilities

Start from one function that:

- reads JSON from a file;
- parses it;
- calculates a total;
- prints the total.

Refactor it into at least:

- file boundary;
- parsing/validation;
- calculation;
- reporting boundary.

Do not invent a trait unless the design genuinely needs one.

## 3. Choose a seam

A program needs the current exchange rate.

Compare:

### Option A

Pass f64 exchange_rate into the pure pricing function.

### Option B

Pass a trait object named ExchangeRateProvider into the pricing function.

State which you would choose for:

1. a function that only needs one already-resolved rate;
2. an application use case that must dynamically fetch different currency pairs during execution.

Explain why.

## 4. Build a small architecture

Create an order-pricing library.

Requirements:

- Order and Money-like domain values;
- pure subtotal calculation;
- discount rule;
- one external tax-rate boundary;
- test fake for tax rate;
- no file, HTTP, or CLI dependencies in the domain module.

Add a small binary that constructs the concrete dependencies and prints a final result.

## Architecture note

Write ARCHITECTURE.md with:

- responsibility of each module or crate;
- dependency arrows;
- state ownership;
- external boundaries;
- why each trait exists;
- one abstraction you deliberately did not add.
