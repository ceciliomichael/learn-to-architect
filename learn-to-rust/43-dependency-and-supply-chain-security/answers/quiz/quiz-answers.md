# Quiz Answers: Module 43

## 1

A package included because one of your dependencies depends on it rather than because your package declared it directly.

## 2

It records the concrete resolved dependency graph that the application tests and ships, making updates and reproduction more deliberate.

## 3

No. Scanners depend on known advisories and rules and cannot prove absence of undisclosed vulnerabilities, malicious behavior, unsafe configuration, or application logic flaws.

## 4

They execute code during the build and can influence generated source, linking, native compilation, and the build environment.

## 5

Procedural macros execute code at compile time to transform Rust syntax.

## 6

No. Reimplementing complex cryptography, TLS, parsing, or protocol code may create more risk than using a mature reviewed dependency.

## 7

What components are present in a software artifact or product.

## 8

Dependency updates can change executed code, features, transitive packages, licenses, build behavior, and vulnerability exposure even when your source files do not change.

## 9

Unused features can bring extra code and transitive dependencies, increasing build and review surface.

## 10

In an appropriate secret-management mechanism outside source control, with the minimum access needed by the build or release process.
