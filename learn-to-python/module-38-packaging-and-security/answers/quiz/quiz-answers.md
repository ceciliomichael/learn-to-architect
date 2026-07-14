# Quiz Answers: Project Structure, Packaging, and Secure Boundaries

1. It prevents accidental imports directly from the project root and tests installed-package behavior.
2. `pyproject.toml`.
3. Package resources may not be ordinary neighboring filesystem paths.
4. No. Loading can execute arbitrary code.
5. It preserves argument boundaries and avoids shell interpretation.
6. The built wheel users will install.
