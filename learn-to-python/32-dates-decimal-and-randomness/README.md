# Module 32: Dates, Time Zones, Decimal, and Randomness

## What you will learn

You will represent dates and instants, calculate exact decimals under explicit rules, and choose ordinary or security randomness.

## Date, time, datetime, and duration

```python
from datetime import date, datetime, timedelta, timezone

today = date(2026, 7, 14)
duration = timedelta(days=2, hours=3)
instant = datetime(2026, 7, 14, 1, 30, tzinfo=timezone.utc)
```

A date is a calendar day. A datetime combines date and time. A timedelta is elapsed duration.

Naive datetime objects have no time-zone information. Aware objects have a `tzinfo` that can locate them relative to UTC. Do not mix naive and aware values without an explicit conversion rule.

## Use zoneinfo for named regions

```python
from zoneinfo import ZoneInfo

manila = ZoneInfo("Asia/Manila")
local = instant.astimezone(manila)
```

Named zones use IANA rules, including historical and future rule data available to the environment. Windows or minimal systems may need the separately installed `tzdata` package. Handle `ZoneInfoNotFoundError` at configuration boundaries.

For a current aware UTC value:

```python
now = datetime.now(timezone.utc)
```

Store instants in UTC when appropriate, but keep a named zone for future local schedules whose intended wall time must follow regional rules.

## Parse and format ISO values

```python
text = instant.isoformat()
restored = datetime.fromisoformat(text)
```

Parsing syntax is not domain validation. Check whether a date-only value, local time, UTC instant, or zoned schedule was required.

## Decimal follows a context

```python
from decimal import Decimal, ROUND_HALF_UP

price = Decimal("12.50")
tax_rate = Decimal("0.08")
total = price * (Decimal("1") + tax_rate)
display = total.quantize(Decimal("0.01"), rounding=ROUND_HALF_UP)
```

Construct Decimal from strings for exact written decimal values. `Decimal(0.1)` captures the float's binary approximation.

Precision and rounding use a context. Use `decimal.localcontext` when a calculation needs temporary settings. Decimal supports exact base-10 arithmetic but business rules still decide rounding timing, currency scale, and exceptional values.

## Random and secrets solve different jobs

```python
import random
random.seed(42)
print(random.randint(1, 6))
```

`random` is deterministic pseudo-randomness suited to simulations, games, sampling, and repeatable tests. It is not secure for tokens or passwords.

```python
import secrets
token = secrets.token_urlsafe(32)
```

Use `secrets` for authentication tokens, password-reset values, and similar security choices. Store token hashes where verification does not require recovering the original.

## Check your understanding

You are ready when you can distinguish a date from an instant, create Decimal from text, and choose secrets for security-sensitive randomness.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
