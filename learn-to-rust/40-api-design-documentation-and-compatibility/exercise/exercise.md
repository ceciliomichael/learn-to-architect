# Exercises: Module 40

## 1. Trace the invariant

Given:

~~~rust
pub struct Port(u16);

impl Port {
    pub fn new(value: u16) -> Result<Self, String> {
        if value == 0 {
            return Err(String::from("port must be nonzero"));
        }
        Ok(Self(value))
    }
}
~~~

Answer:

1. Can another crate construct Port with zero directly?
2. What invariant can a function taking Port rely on?
3. What would become possible if the field were public?

## 2. Repair a weak API

Start with:

~~~rust
pub struct Temperature {
    pub celsius: f64,
}
~~~

Redesign it so construction is explicit, representation is private, read-only access is available, and documentation states that the unit is Celsius.

Do not invent validation rules that were not requested.

## 3. Add executable documentation

Create a small library containing a slug function.

Define a deliberately limited supported behavior:

- trim outer whitespace;
- lowercase ASCII letters;
- replace ASCII spaces with hyphens.

Add rustdoc, one executable example, and tests.

Be explicit that this is not a complete Unicode slugification algorithm.

## 4. Build a Percentage API

Requirements:

- accepted values are 0 through 100;
- invalid construction returns an error;
- the inner value is private;
- a getter is available;
- derive only traits whose semantics make sense;
- documentation contains a usage example;
- there is no public mutable reference to the inner value.

## Compatibility review

Write COMPATIBILITY.md answering:

1. Would changing a private Percentage representation normally break ordinary callers?
2. Would renaming a public constructor break callers?
3. Could changing Display output break consumers?
4. Could adding a variant to a public exhaustive enum break source code?
5. Which parts of your API are intentionally stable?
