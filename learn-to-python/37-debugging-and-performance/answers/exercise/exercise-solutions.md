# Exercise Solutions: Debug, Profile, and Improve Performance

```python
from functools import lru_cache
from timeit import timeit

def running_totals(values: list[int], debug: bool = False) -> list[int]:
    results: list[int] = []
    total = 0
    for value in values:
        total += value
        if debug:
            breakpoint()
        results.append(total)
    return results

print(running_totals([2, 3, 4]))

values_list = list(range(100_000))
values_set = set(values_list)

list_time = timeit(lambda: 99_999 in values_list, number=1_000)
set_time = timeit(lambda: 99_999 in values_set, number=1_000)
print(list_time, set_time)

products = [
    {"product_id": 1, "name": "Pen"},
    {"product_id": 2, "name": "Book"},
]
requested_ids = [2, 1, 2]

products_by_id = {
    product["product_id"]: product
    for product in products
}
selected = [products_by_id[product_id] for product_id in requested_ids]
print(selected)

nested_selected = [
    next(product for product in products if product["product_id"] == product_id)
    for product_id in requested_ids
]
assert selected == nested_selected

@lru_cache(maxsize=256)
def normalize(code: str) -> str:
    return code.strip().casefold()

for _ in range(10):
    normalize(" Sample ")
print(normalize.cache_info())
```

Run `running_totals([2, 3, 4], debug=True)`. At each stop, inspect `value`, `total`, and `results`, then use `n` and `c` to move through the loop. The expected output is `[2, 5, 9]`. A wrong update such as `total = value` becomes visible at the second item. Return to `debug=False` after the investigation.

Save the full example as `performance_practice.py`, then run `python -m cProfile -s cumulative performance_practice.py`. Cumulative time includes time spent in called functions and helps locate an expensive call path. It does not prove why the code is slow, so inspect the top relevant rows and measure a proposed change separately.

The dictionary changes repeated product scans into direct ID lookups while preserving requested order and duplicates. Keep tests for missing IDs and duplicate requests before and after the change.

`cache_info` reports one miss followed by nine hits for the repeated normalized text. The maximum size bounds retained entries. Cache only when values are safe to retain and results do not depend on changing external state. Compare timings only in the same environment and keep correctness tests green.
