# Module 21: Virtual Environments and Dependencies

## What you will learn

You will isolate project packages, install through the intended interpreter, and record dependency decisions.

## Why environments matter

Two projects may require different versions of the same package. A virtual environment gives one project its own interpreter context and installed packages while reusing the base Python installation.

From a project root:

```text
python -m venv .venv
```

Activate in PowerShell:

```text
.\.venv\Scripts\Activate.ps1
```

Activate in a POSIX shell:

```text
source .venv/bin/activate
```

Activation mainly changes shell path lookup. You can always call the environment interpreter directly. Do not commit `.venv`; recreate it from dependency records.

## Confirm the interpreter

```text
python -c "import sys; print(sys.executable)"
python -m pip --version
```

Using `python -m pip` ties pip to the displayed interpreter and avoids installing into a different Python accidentally.

## Install only intentional packages

```text
python -m pip install package-name
```

Check the official project, maintainers, release history, documentation, license, vulnerabilities, and exact spelling before installing. Package installation can run build code, so treat dependencies as code execution and supply-chain trust.

## Record direct and resolved dependencies

For small controlled exercises:

```text
python -m pip freeze > requirements.txt
python -m pip install -r requirements.txt
```

`freeze` records everything installed, including transitive packages, but does not explain which dependencies are direct. Production teams often use a lock-capable workflow that records hashes and platform resolution while keeping direct requirements separately documented.

Do not casually update all versions. Review changelogs, compatibility, security, and tests.

## Deactivate and recreate

```text
deactivate
```

To prove reproducibility, create a fresh environment, install recorded dependencies, and run tests. Never repair a broken environment by committing its installed files.

## Secrets do not belong in environments or requirements

A virtual environment is not a secret store. Use protected environment configuration or an approved secret manager, and keep credentials out of commands, shell history, logs, and source control.

## Check your understanding

You are ready when you can prove which interpreter pip targets and recreate a clean environment from reviewed records.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
