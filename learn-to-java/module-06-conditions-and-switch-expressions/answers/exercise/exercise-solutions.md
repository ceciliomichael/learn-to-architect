# Exercise solution

```java
public class Main {
    public static void main(String[] args) {
        int score = 82;
        String level = switch (score / 10) {
            case 10, 9 -> "excellent";
            case 8, 7 -> "good";
            default -> "practice";
        };
        System.out.println(level);
    }
}
```

Choose program paths from explicit boolean and domain cases. The program demonstrates each rule listed in the lesson and produces good.

For the practice extension, change one behavior at a time and recompile immediately. If your implementation differs, it is still correct when it preserves validation, ownership, and observable behavior.

