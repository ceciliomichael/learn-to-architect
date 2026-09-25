# Exercise Solutions: Module 35

Attempt the exercises before reading.

## 1. Trace

The channel is considered connected while any sender exists, so the receiver cannot conclude that no future message will arrive.

## 2. Repair

Ensure sender ownership follows the shutdown lifecycle. Drop or move every sender before relying on receiver disconnection.

## 3. Modify

Clone the sender before spawning producers, move one clone into each, and do not assume which producer's messages arrive first.

## 4. Build

Use the enum when explicit protocol state improves clarity. Closure remains useful as a final signal that no senders survive. Bounded capacity prevents unlimited queued work.

Equivalent implementations can be correct when they satisfy the same behavior and constraints.
