# Exercise Solutions: Module 14

Attempt the work first.

## 1. Trace

The value is Ok(u32) or Err(String). ? extracts the Ok value and continues, or returns the Err early from the current function when types are compatible.

## 2. Repair

Change the function signature to return Result, map or preserve the parse error, and match the result at the reporting boundary.

## 3. Modify

After parsing, compare against the chosen maximum and return a domain Err before Ok. Parsing and validation remain separate failure reasons.

## 4. Build

Parse u16, map the parsing failure to useful context, reject zero as a domain rule, return Ok(port) otherwise, and report once in main.

Equivalent designs can be correct when they satisfy the same rules and behavior.
