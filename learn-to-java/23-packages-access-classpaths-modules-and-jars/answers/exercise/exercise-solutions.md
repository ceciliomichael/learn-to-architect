# Exercise solution

```java
public class Main {
    public static void main(String[] args) {
        Module module = Main.class.getModule();
        Package location = Main.class.getPackage();
        System.out.println("named module: " + module.isNamed());
        System.out.println("package: " + location.getName());
    }
}
```

Organize source and compiled code so names, visibility, and runtime lookup agree. This solution enforces the lesson contracts and has the expected behavior: named module: false and an empty package name.

The extension should be implemented one rule at a time with the relevant test or compiler check rerun after each change. Dependency versions shown here are explicit inputs and should be reviewed during future updates.

