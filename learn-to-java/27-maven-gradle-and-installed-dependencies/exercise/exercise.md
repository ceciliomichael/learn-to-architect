# Exercise: Maven, Gradle, and Installed Dependencies

1. Recreate the example in a disposable project using the documented source layout.
2. Run or verify it with mvn test, then mvn dependency:tree.
3. Confirm this behavior: a Java 21 build with JUnit available only to tests.
4. Inspect the resolved tree and local repository, then explain why downloaded files are generated inputs rather than source files to commit.
5. Explain how every listed contract is enforced and what would break if it were removed.

Do not commit generated caches, downloaded libraries, credentials, or real user data.

