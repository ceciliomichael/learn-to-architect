# Exercise solution

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] scores = {82, 91, 74};
        int[] copy = Arrays.copyOf(scores, scores.length);
        copy[0] = 100;
        String label = args.length == 0 ? "scores" : args[0];
        System.out.println(label + ": " + Arrays.toString(scores));
        System.out.println(Arrays.toString(copy));
    }
}
```

Use fixed-length sequences and check every external index before reading it. The program demonstrates each rule listed in the lesson and produces the original scores followed by an independent copy beginning with 100.

For the practice extension, change one behavior at a time and recompile immediately. If your implementation differs, it is still correct when it preserves validation, ownership, and observable behavior.

