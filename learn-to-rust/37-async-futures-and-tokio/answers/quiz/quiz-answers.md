# Quiz Answers: Module 37

## 1

No. It constructs a Future; a runtime decides how tasks are scheduled onto runtime threads.

## 2

Suspend the current future while other ready tasks can make progress.

## 3

It occupies a runtime worker thread instead of cooperatively yielding, reducing or stalling progress for other tasks.

## 4

No. It stops waiting or cancels the wrapped future according to its semantics, but completed external or local side effects may remain.

## 5

Unbounded tasks can exhaust memory, sockets, remote services, queues, or other finite resources even when each individual task is asynchronous.
