# Exercise solution

```java
public class Main {
    public static void main(String[] args) {
        String name = "Java";
        String separate = new String("Java");
        String note = """
                Learn carefully.
                Practice daily.
                """;
        System.out.println(name.equals(separate));
        System.out.println(name.codePointCount(0, name.length()));
        System.out.print(note);
    }
}
```

Handle text without assuming one char always equals one visible symbol. The program demonstrates each rule listed in the lesson and produces true, 4, and two note lines.

For the practice extension, change one behavior at a time and recompile immediately. If your implementation differs, it is still correct when it preserves validation, ownership, and observable behavior.

