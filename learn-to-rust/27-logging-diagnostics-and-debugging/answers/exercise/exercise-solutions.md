# Exercise Solutions: Module 27

Attempt the exercises before reading.

## 1. Trace

Logging and returning at many layers creates duplicate records and unclear ownership. Let lower layers preserve the error; log where useful operation context and reporting policy are known.

## 2. Repair

Log an account or request identifier, error category, or operation name instead of the credential itself.

## 3. Modify

Include request_id as an instrumented argument or explicit field, and propagate it through relevant operations without treating it as a secret if your domain permits logging it.

## 4. Build

Keep processing logic Result-based. Establish a batch span and add item identifiers as fields. Avoid payload dumps and duplicate stack-layer logs.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
