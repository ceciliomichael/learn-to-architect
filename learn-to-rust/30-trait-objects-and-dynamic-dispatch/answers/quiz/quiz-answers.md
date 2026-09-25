# Quiz Answers: Module 30

## 1

When runtime-selected heterogeneous implementations need one common interface.

## 2

Trait-object calls select implementation at runtime through indirection, while generics retain concrete types for compile-time specialization.

## 3

No. The outer trait-object type is uniform while concrete implementers can differ.

## 4

It suggests callers actually depend on concrete types that the supposed shared interface did not model well.

## 5

No. Use it when runtime heterogeneity or boundary decoupling provides real value.
