# Exercise solution

Use this release record and fill it with values produced by your own environment:

```text
Local release record

Checks:
- cargo fmt --check
- cargo clippy --all-targets --all-features -- -D warnings
- cargo test --all-features
- cargo build --release --locked

Bundle contents:
- application executable from target/release
- README.md
- LICENSE
- config.example without credentials

Provenance:
- application version
- source commit, when Git is used
- complete rustc --version --verbose output
- target triple
- exact build command
- Cargo.lock checksum
- executable SHA-256 checksum

Startup verification:
- run --help
- start with example configuration
- perform one harmless normal operation
- confirm useful stderr output and nonzero status for invalid configuration
- confirm clean shutdown

Rollback:
- stop the new process safely
- restore the previous known-good artifact and configuration
- repeat startup verification
- record why rollback occurred
```

PowerShell can generate a checksum with `Get-FileHash -Algorithm SHA256 PATH`. Linux commonly provides `sha256sum PATH`. Use the command appropriate to the release environment and record which tool produced the value.
