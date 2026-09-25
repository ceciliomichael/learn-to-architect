# Exercise Solutions: Module 43

## 1. Trace a dependency

There is no universal graph answer because it depends on your project.

A correct response identifies real packages from cargo tree and explains the chain that introduced them.

The purpose of reverse-tree inspection is to answer:

**Why is this package present?**

not merely:

**Is this package present?**

## 2. Review an update

A strong update review includes:

- old and new resolved versions;
- lock-file changes;
- graph changes;
- feature changes;
- test results;
- lint/check results;
- any behavior or migration concern.

Treat dependency changes as software changes even when application source is untouched.

## 3. Dependency adoption review

A strong review is factual.

Do not fill unknown license, maintenance, or security details from memory.

The point is to establish a repeatable evaluation method and make trust assumptions visible.

## 4. SBOM plan

An SBOM plan should identify the shipped artifact and the components needed to understand what is inside it.

An SBOM complements vulnerability scanning and dependency review.

It does not replace either one.
