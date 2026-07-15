# Exercise: Prepare a local release bundle

Use one of your Cargo application projects.

1. Run formatting, Clippy, tests, and a locked release build.
2. Create a clean local bundle directory containing only the executable, README, license, and example configuration without secrets.
3. Record the source commit if the project uses Git, `rustc --version --verbose`, target, and build command.
4. Generate a SHA-256 checksum using an operating-system tool available to you.
5. Write startup verification and rollback steps. Do not publish or deploy the bundle.
