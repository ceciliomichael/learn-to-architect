# Exercise Solutions: Virtual Environments and Dependencies

```text
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -c "import sys; print(sys.executable)"
python -m pip --version
python -m pip list
python -m pip freeze > requirements.txt
deactivate
python -m venv .venv-check
.\.venv-check\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

Use the POSIX activation path when not in PowerShell. The exercise environment may contain only pip and its support packages, which is a valid result. Add:

```text
.venv/
.venv-check/
```

to `.gitignore` because environments are generated, platform-specific, and reproducible from dependency records.
