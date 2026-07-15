# Exercise: Debuggers, Sanitizers, and Static Analysis

## Steps

1. Build with -g and step through find_index in a debugger.
2. Test the first value, last value, and a missing value.
3. Run supported address and undefined-behavior sanitizers.
4. Run GCC -fanalyzer or another available static analyzer.
5. Record what each tool observed and what still depends on tests.

## Success check

First, last, and missing paths run, strict warnings remain clean, and supported tools report no violation.

