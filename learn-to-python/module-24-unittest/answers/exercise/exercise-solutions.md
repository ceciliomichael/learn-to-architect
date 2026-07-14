# Exercise Solutions: Test with unittest

`practice.py`:

```python
from pathlib import Path

class MissingSettingError(Exception):
    pass

def subtotal(price: float, quantity: int) -> float:
    if price < 0 or quantity < 0:
        raise ValueError("price and quantity must be nonnegative")
    return price * quantity

def normalize(text: str) -> str:
    return " ".join(text.split()).casefold()

def required_setting(settings: dict[str, str], name: str) -> str:
    try:
        return settings[name]
    except KeyError as error:
        raise MissingSettingError(f"missing setting: {name}") from error

def write_note(path: Path, text: str) -> None:
    path.write_text(text, encoding="utf-8")
```

`test_practice.py`:

```python
from pathlib import Path
from tempfile import TemporaryDirectory
import unittest

from practice import MissingSettingError, normalize, required_setting, subtotal, write_note

class PracticeTests(unittest.TestCase):
    def test_subtotal_with_ordinary_values(self) -> None:
        self.assertEqual(subtotal(12.5, 3), 37.5)

    def test_subtotal_with_zero_quantity(self) -> None:
        self.assertEqual(subtotal(12.5, 0), 0)

    def test_subtotal_rejects_negative_quantity(self) -> None:
        with self.assertRaisesRegex(ValueError, "nonnegative"):
            subtotal(12.5, -1)

    def test_normalize_handles_empty_and_unicode_text(self) -> None:
        self.assertEqual(normalize("   "), "")
        self.assertEqual(normalize("  MA\u00d1ANA  "), "ma\u00f1ana")

    def test_required_setting_raises_domain_error(self) -> None:
        with self.assertRaisesRegex(MissingSettingError, "token"):
            required_setting({}, "token")

    def test_write_note_uses_the_given_directory(self) -> None:
        with TemporaryDirectory() as directory:
            path = Path(directory) / "note.txt"
            write_note(path, "Clear test")
            self.assertEqual(path.read_text(encoding="utf-8"), "Clear test")

if __name__ == "__main__":
    unittest.main()
```

Run `python -m unittest discover -v`. To study a useful failure, temporarily change the expected ordinary subtotal to `40.0`, run the suite, read the expected and actual values, then restore `37.5` and confirm the suite passes. The temporary directory gives the file test a fresh boundary and cleans it afterward.
