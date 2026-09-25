# Exercise Solutions: Module 20

Attempt the exercises before reading.

## 1. Trace

Article must implement title. It can inherit summarize because the default implementation is expressed in terms of title.

## 2. Repair

Require std::fmt::Debug on T. Do not add Clone or other unrelated capabilities.

## 3. Modify

Implement Summary for Video. The generic caller remains unchanged because it depends on the trait contract.

## 4. Build

Each domain type owns its validation rules. The generic function depends only on Validatable and can propagate or collect errors according to a stated contract.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
