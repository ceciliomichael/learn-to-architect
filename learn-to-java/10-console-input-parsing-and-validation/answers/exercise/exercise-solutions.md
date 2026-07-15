# Exercise solution

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        try (Scanner scanner = new Scanner(System.in)) {
            System.out.print("Quantity: ");
            String text = scanner.nextLine().trim();
            try {
                int quantity = Integer.parseInt(text);
                if (quantity < 1 || quantity > 100) {
                    System.out.println("Use a quantity from 1 through 100.");
                    return;
                }
                System.out.println("Accepted: " + quantity);
            } catch (NumberFormatException error) {
                System.out.println("Enter a whole number.");
            }
        }
    }
}
```

Separate reading text, converting its shape, and validating its domain meaning. The program demonstrates each rule listed in the lesson and produces a prompt and either accepted input or a correction message.

For the practice extension, change one behavior at a time and recompile immediately. If your implementation differs, it is still correct when it preserves validation, ownership, and observable behavior.

