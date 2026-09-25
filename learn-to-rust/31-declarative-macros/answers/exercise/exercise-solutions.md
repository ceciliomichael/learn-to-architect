# Exercise Solutions: Module 31

Attempt the exercises before reading.

## 1. Trace

Macro repetition operates over syntax before a function signature exists. A normal function has a statically defined parameter list unless values are first grouped into a collection or tuple.

## 2. Repair

Use expr when the caller should supply an arbitrary expression. Use ident only when the API truly requires an identifier rather than a general expression.

## 3. Modify

Give the generated result an explicit Vec<String> type, or invoke it in a context that constrains the element type.

## 4. Build

The macro can expand to an if check with return Err(...). It is justified only if the desired early-return control-flow syntax is meaningfully clearer than repeated ordinary code; otherwise a function is easier to understand.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
