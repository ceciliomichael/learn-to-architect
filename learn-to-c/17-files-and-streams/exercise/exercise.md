# Exercise: Files and Streams

## Goal

Apply the module's rules in a complete program that you can explain line by line.

## Steps

1. Open exercise-data.txt for writing.
2. Write two labeled integer lines and check fprintf.
3. Require fclose to succeed.
4. Reopen the file for reading and print both lines with a bounded buffer.
5. Handle open, read, and close failure without using a stream after it is closed.

## Success check

The program verifies each file boundary, prints both stored lines, and closes each successfully opened stream exactly once.

Use the same strict C17 command from the lesson unless a step says otherwise. Attempt the work before opening the solution.

