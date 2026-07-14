# Exercise solution

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

Group related state and behavior without hiding how objects and references work. The program demonstrates each rule listed in the lesson and produces 1.

For the practice extension, change one behavior at a time and recompile immediately. If your implementation differs, it is still correct when it preserves validation, ownership, and observable behavior.

