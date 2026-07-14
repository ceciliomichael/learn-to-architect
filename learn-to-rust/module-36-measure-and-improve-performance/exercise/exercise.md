# Exercise: Remove repeated allocation

Compare two functions that join the strings `"item-0"` through `"item-9999"` into one output.

1. The first repeatedly uses `output = output + &piece`.
2. The second creates one mutable `String`, reserves reasonable capacity, and uses `push_str`.
3. Confirm both outputs are equal.
4. Time each with `std::time::Instant` in a release build for several runs.
5. Record the environment and results. Do not claim a universal speed ratio from one machine.
