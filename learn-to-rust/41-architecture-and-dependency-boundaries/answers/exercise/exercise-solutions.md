# Exercise Solutions: Module 41

## 1. Trace dependency direction

The pricing domain should normally not need reqwest types when its responsibility is pricing policy rather than transport.

The HTTP adapter or orchestration layer should convert the external payload into validated domain inputs.

The concrete HTTP client is usually created near the application composition root, often main or a top-level application constructor.

## 2. Repair mixed responsibilities

A clean flow is:

~~~text
read file
   |
   v
raw text
   |
   v
parse and validate
   |
   v
domain values
   |
   v
calculate
   |
   v
result
   |
   v
print/report
~~~

The exact functions depend on the application.

The important part is that the calculation can be tested without a file and that the parser can be tested without terminal output.

## 3. Choose a seam

For a pure function that only needs one already-resolved rate, passing the numeric or domain rate value is simpler and more explicit.

For an application use case that actively needs to resolve several rates dynamically, a provider capability may be justified around that external lookup.

Do not make the lowest-level arithmetic function responsible for remote lookup unless that is truly its job.

## 4. Build a small architecture

A valid shape is:

~~~text
binary
 |
 +--> tax adapter
 |
 v
application/pricing
 |
 v
domain
~~~

Domain calculation should accept values or a narrow capability according to the exact use case.

Tests use controlled input and avoid real external I/O.

A different structure can be correct if it preserves clear responsibilities and dependency direction.
