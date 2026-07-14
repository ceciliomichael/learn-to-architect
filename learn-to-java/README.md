# Learn Java Step by Step

This course teaches Java from the beginning through maintainable production work. No prior programming experience is required.

## Language baseline

Examples target Java 21 and newer. Java 21 is an established LTS release with the permanent modern features used here. If your installed JDK is newer, compile course examples with:

```text
javac --release 21 -Xlint:all Main.java
java Main
```

This tests the Java 21 language and API contract instead of silently using newer host features. Optional notes may describe newer releases, but required exercises do not depend on them.

## Online and local compilers

For early single-file lessons, use the official [Java Playground](https://dev.java/playground/). It is a sandbox and is not suitable for private code, installed dependencies, multiple-file builds, local files, databases, profiling, or packaging.

For local work, install a maintained JDK distribution and verify `java -version` and `javac -version`. The JDK contains development tools; a runtime alone is not enough to compile.

## How modules work

Each module has a lesson, guided exercise, quiz, complete exercise solution, and explained quiz answers. Follow the order because the course does not use a feature before establishing its prerequisites.

## Course path

- [Module 01: Playground, JDK Choices, and Tool Versions](module-01-playground-jdk-choices-and-tool-versions/README.md)
- [Module 02: Source Files, Compilation, Class Files, and Main](module-02-source-compilation-class-files-and-main/README.md)
- [Module 03: Variables, Primitive Types, and Constants](module-03-variables-primitive-types-and-constants/README.md)
- [Module 04: Strings, Characters, Unicode, and Text Blocks](module-04-strings-characters-unicode-and-text-blocks/README.md)
- [Module 05: Operators, Conversions, Overflow, and Math](module-05-operators-conversions-overflow-and-math/README.md)
- [Module 06: Conditions and Switch Expressions](module-06-conditions-and-switch-expressions/README.md)
- [Module 07: Loops and Repetition](module-07-loops-and-repetition/README.md)
- [Module 08: Methods, Parameters, Return Values, and Scope](module-08-methods-parameters-return-values-and-scope/README.md)
- [Module 09: Arrays and Command-Line Arguments](module-09-arrays-and-command-line-arguments/README.md)
- [Module 10: Console Input, Parsing, and Validation](module-10-console-input-parsing-and-validation/README.md)
- [Module 11: Classes and Objects](module-11-classes-and-objects/README.md)
- [Module 12: Constructors, Encapsulation, and Invariants](module-12-constructors-encapsulation-and-invariants/README.md)
- [Module 13: Immutability and Records](module-13-immutability-and-records/README.md)
- [Module 14: Enums, Sealed Types, and Pattern Matching](module-14-enums-sealed-types-and-pattern-matching/README.md)
- [Module 15: Exceptions and Resource Cleanup](module-15-exceptions-and-resource-cleanup/README.md)
- [Module 16: Lists, Sets, and Maps](module-16-lists-sets-and-maps/README.md)
- [Module 17: Generics and Type Bounds](module-17-generics-and-type-bounds/README.md)
- [Module 18: Interfaces and Composition](module-18-interfaces-and-composition/README.md)
- [Module 19: Inheritance and Polymorphism](module-19-inheritance-and-polymorphism/README.md)
- [Module 20: Equality, Hashing, and Ordering](module-20-equality-hashing-and-ordering/README.md)
- [Module 21: Lambdas and Functional Interfaces](module-21-lambdas-and-functional-interfaces/README.md)
- [Module 22: Streams and Optional Values](module-22-streams-and-optional-values/README.md)
- [Module 23: Packages, Access, Classpaths, Modules, and JARs](module-23-packages-access-classpaths-modules-and-jars/README.md)
- [Module 24: Files, Paths, and Buffered I/O](module-24-files-paths-and-buffered-io/README.md)
- [Module 25: Date, Time, Locale, and Formatting](module-25-date-time-locale-and-formatting/README.md)
- [Module 26: Regular Expressions and Text Processing](module-26-regular-expressions-and-text-processing/README.md)
- [Module 27: Maven, Gradle, and Installed Dependencies](module-27-maven-gradle-and-installed-dependencies/README.md)
- [Module 28: Testing with JUnit](module-28-testing-with-junit/README.md)
- [Module 29: JSON and Untrusted Data](module-29-json-and-untrusted-data/README.md)
- [Module 30: HTTP Clients and Network Boundaries](module-30-http-clients-and-network-boundaries/README.md)
- [Module 31: JDBC, Connection Pools, and Transactions](module-31-jdbc-connection-pools-and-transactions/README.md)
- [Module 32: Threads, Executors, Futures, and Completion](module-32-threads-executors-futures-and-completion/README.md)
- [Module 33: Virtual Threads and Task Ownership](module-33-virtual-threads-and-task-ownership/README.md)
- [Module 34: Synchronization and Concurrent Collections](module-34-synchronization-and-concurrent-collections/README.md)
- [Module 35: Reflection, Annotations, and Runtime Types](module-35-reflection-annotations-and-runtime-types/README.md)
- [Module 36: JVM Memory, Garbage Collection, and Resources](module-36-jvm-memory-garbage-collection-and-resources/README.md)
- [Module 37: Measurement, JFR, and JMH](module-37-measurement-jfr-and-jmh/README.md)
- [Module 38: Command-Line Configuration and Logging](module-38-command-line-configuration-and-logging/README.md)
- [Module 39: Documentation, API Compatibility, and Dependency Security](module-39-documentation-api-compatibility-and-dependency-security/README.md)
- [Module 40: Build, Package, and Release Java Programs](module-40-build-package-and-release/README.md)

Installed third-party packages are taught directly in Module 27, after learners understand packages, JARs, and classpaths. The JUnit and JSON modules then use real dependencies through that reproducible build.

There is intentionally no miscellaneous module or final assessment.
