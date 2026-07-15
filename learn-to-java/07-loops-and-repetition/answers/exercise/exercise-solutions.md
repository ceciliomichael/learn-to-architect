# Exercise solution

```java
public class Main {
    public static void main(String[] args) {
        int total = 0;
        for (int number = 1; number <= 5; number++) {
            total += number;
        }
        System.out.println(total);
    }
}
```

Repeat work with a visible starting state, continuation rule, and progress step. The program demonstrates each rule listed in the lesson and produces 15.

For the practice extension, change one behavior at a time and recompile immediately. If your implementation differs, it is still correct when it preserves validation, ownership, and observable behavior.

