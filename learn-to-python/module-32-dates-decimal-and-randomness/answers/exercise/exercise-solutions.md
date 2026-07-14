# Exercise Solutions: Dates, Time Zones, Decimal, and Randomness

```python
from datetime import datetime, timedelta, timezone
from decimal import Decimal, ROUND_HALF_UP
import random
import secrets
from zoneinfo import ZoneInfo

instant = datetime(2026, 7, 14, 1, 30, tzinfo=timezone.utc)
manila = instant.astimezone(ZoneInfo("Asia/Manila"))
print(instant.isoformat())
print(manila.isoformat())
print((instant + timedelta(hours=36)).isoformat())

subtotal = Decimal("37.50")
tax = subtotal * Decimal("0.08")
total = (subtotal + tax).quantize(Decimal("0.01"), rounding=ROUND_HALF_UP)
print(total)
print(Decimal("0.1"))
print(Decimal(0.1))

random.seed(42)
print([random.randint(1, 6) for _ in range(5)])
print(secrets.token_urlsafe(32))
```

Adding 36 hours changes the instant by exactly 36 elapsed hours. A local calendar rule such as "same local time tomorrow" is different when a region's clock changes and should be modeled from the named zone and business rule. The shown dates do not cross a clock change, but the distinction still matters for other zones and date ranges.

`Decimal("0.1")` starts from exact decimal text. `Decimal(0.1)` preserves the float's earlier binary approximation, so it displays many digits. The invoice explicitly rounds to two decimal places with `ROUND_HALF_UP`.

The seeded ordinary random sequence is repeatable and useful for simulations or tests. The secrets token is intentionally not reproducible and is the correct family for security-sensitive tokens.
