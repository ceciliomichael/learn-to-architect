# Module 11: Classes and Objects

## Why this matters

Group related state and behavior without hiding how objects and references work.

## Rules to learn

- **class:** A class declares the fields and methods available to its instances.
- **object:** new creates an object and returns a reference to it.
- **instance field:** Each object has its own instance-field values unless a field is static.
- **method receiver:** An instance method acts on the object referenced by this.
- **reference sharing:** Assigning an object reference does not clone the object.

## Complete example

```java
public class Main {
    static class Counter {
        int value;

        void increment() {
            value++;
        }
    }

    public static void main(String[] args) {
        Counter first = new Counter();
        Counter alias = first;
        alias.increment();
        System.out.println(first.value);
    }
}
```

Compile with `javac --release 21 -Xlint:all Main.java` and run with `java Main`. Expected behavior: 1.

## Deliberate practice

Create a second independent Counter and prove that changing it does not affect first.

Type the code instead of pasting it. Predict the result first, then use compiler feedback to check your reasoning.

Continue to [Module 12](../module-12-constructors-encapsulation-and-invariants/README.md).

