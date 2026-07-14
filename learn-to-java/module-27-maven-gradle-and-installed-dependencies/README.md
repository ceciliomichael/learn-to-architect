# Module 27: Maven, Gradle, and Installed Dependencies

## Why this matters

Install and resolve third-party Java libraries through a reproducible project build, not by copying random JAR files.

## Contracts to learn

- **coordinates:** A dependency is identified by group, artifact, and version coordinates.
- **scope:** A scope or configuration states whether code is needed for compilation, tests, runtime, or another phase.
- **transitive graph:** One direct dependency can bring many transitive dependencies that also require review.
- **wrapper:** A committed Maven or Gradle wrapper pins the build-tool distribution for the project.
- **trust:** Review source, maintainers, license, advisories, checksums, build plugins, and resolved changes before approval.

## Complete example

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0">
  <modelVersion>4.0.0</modelVersion>
  <groupId>course</groupId>
  <artifactId>dependency-practice</artifactId>
  <version>1.0.0-SNAPSHOT</version>
  <properties>
    <maven.compiler.release>21</maven.compiler.release>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
  <dependencies>
    <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter</artifactId>
      <version>6.1.2</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.15.0</version>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>3.5.5</version>
      </plugin>
    </plugins>
  </build>
</project>
```

Run or verify this example with mvn test, then mvn dependency:tree. JUnit 6 requires Maven Surefire 3.0.0 or newer, so the example pins a tested plugin version instead of depending on Maven's changing defaults. Expected behavior: a Java 21 build with JUnit available only to tests.

## Deliberate practice

Inspect the resolved tree and local repository, then explain why downloaded files are generated inputs rather than source files to commit.

Keep build files and resolved dependency changes under review. Do not weaken a validator or suppress a diagnostic merely to make an example pass.

Continue to [Module 28](../module-28-testing-with-junit/README.md).
