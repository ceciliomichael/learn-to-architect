# Exercise solution

A complete review should use this structure:

```text
Dependency: serde
Need: Derive well-tested serialization contracts for JSON boundary types.
Standard library alternative: No general serialization framework is provided.
Source and owner: Record the official repository and current maintainers.
License: Record the published license and confirm project compatibility.
Selected version: Copy the exact version from Cargo.lock.
Features: List direct features and the output of cargo tree -e features.
Build behavior: Record build.rs and procedural macro crates in the graph.
Maintenance evidence: Record recent releases, issue handling, and advisories.
Update plan: Update in a small change, review the diff, run all target tests and audits.
Rollback plan: Restore the reviewed lock file and release artifact if validation fails.
Decision: Approve, reject, or request more evidence, with a reason.
```

Values such as maintainers and versions must be collected when the review occurs because they can change. Evidence links should point to the official repository, registry entry, license, and advisory source.
