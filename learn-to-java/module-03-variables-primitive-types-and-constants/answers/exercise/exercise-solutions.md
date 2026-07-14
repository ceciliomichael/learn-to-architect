# Exercise solution

```java
public class Main {
    public static void main(String[] args) {
        int lessons = 3;
        long visitors = 2_000_000L;
        double price = 19.95;
        boolean open = true;
        char grade = 'A';
        final int maxLessons = 40;
        System.out.printf("%d %d %.2f %b %c %d%n",
                lessons, visitors, price, open, grade, maxLessons);
    }
}
```

Store values with types that match their meaning and make reassignment rules visible. The program demonstrates each rule listed in the lesson and produces 3 2000000 19.95 true A 40.

For the practice extension, change one behavior at a time and recompile immediately. If your implementation differs, it is still correct when it preserves validation, ownership, and observable behavior.

