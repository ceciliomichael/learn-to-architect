# Exercise solution

```java
public class Main {
    sealed interface Result permits Success, Failure {}
    record Success(int value) implements Result {}
    record Failure(String message) implements Result {}

    static String describe(Result result) {
        return switch (result) {
            case Success(int value) -> "value " + value;
            case Failure(String message) -> "error " + message;
        };
    }

    public static void main(String[] args) {
        System.out.println(describe(new Success(42)));
    }
}
```

Represent a closed set of domain states so the compiler can check exhaustive handling. The program demonstrates each rule listed in the lesson and produces value 42.

For the practice extension, change one behavior at a time and recompile immediately. If your implementation differs, it is still correct when it preserves validation, ownership, and observable behavior.

