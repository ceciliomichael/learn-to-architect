# Plan for the Programming Concepts (ProgCon) Learning Module

## Purpose

This document is the source of truth for building `learn-to-progcon/`, a complete beginner course in programming concepts. It records the course goals, teaching rules, module order, file structure, and completion checks.

ProgCon stands for Programming Concepts. The course teaches how to think through problems, design solutions with pseudocode and flowcharts, use structured programming, and only then implement those designs in Python. No prior programming experience is required.

The course is inspired by a college Programming Concepts outline covering algorithms, variables, structured design, selection, loops, arrays, and an introduction to Python. This plan expands that outline into a proper learning module curriculum with the same rigor used in the TypeScript and Python courses in this repository.

## Course findings that shape the design

Many first programming courses jump into a language syntax before learners can describe a solution clearly. Others teach flowchart shapes without enough practice following logic by hand. This course corrects both problems.

1. Problem solving and the program development cycle come before any language syntax.
2. Algorithms are taught as precise, ordered, finite instructions, not as vague "steps."
3. Pseudocode and flowcharts are treated as design tools, not decoration.
4. Variables, constants, assignment, and arithmetic are practiced with trace tables before branching.
5. Modules and hierarchy charts teach decomposition before complex control flow piles up.
6. The three basic structures (sequence, selection, loop) are named and practiced explicitly.
7. Selection is split across boolean expressions, relational and logical operators, and nested or multi-way decisions.
8. Loops cover control variables, while and for forms, definite and indefinite cases, nesting, and common mistakes.
9. Arrays include memory layout ideas, indexing, searching, parallel arrays, and loop-based processing.
10. Python arrives only after design skills are solid. Learners convert earlier designs into running code.
11. A capstone module requires a full design-to-code path, not only a last-minute coding sprint.

## Course promise

A learner who follows the modules in order should be able to:

- explain what a computer program is and how the program development cycle works
- write an algorithm that is ordered, precise, and finite
- design a solution in pseudocode and as a flowchart
- use variables, constants, assignment, and arithmetic correctly
- desk-check logic with a trace table before running code
- break a solution into modules and show the structure with a hierarchy chart
- recognize spaghetti code and rewrite it with sequence, selection, and loop structures
- write single-alternative, dual-alternative, and multi-way selection logic
- evaluate boolean expressions with relational and logical operators, including range checks
- design while and for loops, including nested loops, without common control mistakes
- model related data with arrays, search them, and process them with loops
- translate a flowchart or pseudocode design into working Python
- complete a small end-to-end project from problem statement to running program

## Non-negotiable writing rules

Every course file must follow these rules:

1. Use no emoji.
2. Use no em dash character.
3. Prefer short, direct sentences.
4. Introduce one main idea at a time.
5. Define a new word when it first appears.
6. Do not use an analogy unless it makes the idea easier to understand.
7. Do not describe ordinary design work with inflated words such as enterprise, production-grade, or architectural.
8. Do not claim that pseudocode or flowcharts replace testing. Explain what each tool checks and what it cannot check.
9. Do not present style preferences as universal laws.
10. Keep design language and implementation language clearly separated until the Python modules.
11. Use examples with familiar subjects such as grades, prices, temperatures, shopping totals, attendance, and simple messages.
12. Keep examples small enough to understand without unrelated detail.
13. Never require syntax that has not been taught, unless the line is clearly marked as a preview and is not required for practice.
14. Represent flowcharts in text with clear symbol names and simple diagrams learners can redraw on paper.
15. Use inclusive, calm language. Errors and wrong traces are information, not failure.

## Learning pattern for every module

Each module keeps this folder layout:

```text
NN-topic-name/
  README.md
  exercise/
    exercise.md
  quiz/
    quiz.md
  answers/
    exercise/
      exercise-solutions.md
    quiz/
      quiz-answers.md
```

Every lesson follows this order:

1. `Before you start`: lists only the required earlier ideas.
2. `What you will learn`: two to five concrete outcomes.
3. `Why this matters`: a short, ordinary reason to learn the topic.
4. Lesson sections: explain, show a small example, and let the learner predict a result.
5. `Common mistakes`: likely errors and how to correct them.
6. `Check your understanding`: short questions answerable from the lesson.
7. `Practice`: links to the module practice and quiz.
8. `Next step`: one short description of what follows.

Every exercise file contains:

1. a warm-up that changes a working example
2. a guided exercise with numbered steps
3. an independent exercise with observable requirements
4. a debugging or desk-check task when it suits the topic
5. a completion checklist
6. a link to the exercise solutions

Every quiz file contains:

1. questions that only use the current and earlier lessons
2. a mix of prediction, explanation, comparison, and small design-reading questions
3. no interview trivia
4. no concepts from later modules
5. a link to the quiz answers

Every answer file contains:

1. a complete solution for every task
2. a plain explanation of the important choices
3. expected output, expected trace results, or expected design structure when relevant
4. one valid alternative when it teaches a useful distinction
5. no unrelated advanced syntax

## Course structure

The course lives in `learn-to-progcon/`. The root contains:

- `README.md`: course introduction, study routine, tools, and module map
- numbered module folders such as `01-computers-programs-and-environments`
- no miscellaneous folder

## Curriculum roadmap

### Part 1: Foundations of programming thinking

- [x] **Module 01: Computers, Programs, and Environments**
  - Prerequisites: none
  - Teaches: computer system components, hardware vs software, programs, source vs running result, programming environments, and user environments
  - Outcome: the learner can describe what a program is and name the main parts of a computer system

- [x] **Module 02: Problem Solving and the Program Development Cycle**
  - Prerequisites: Module 01
  - Teaches: understanding the problem, planning, coding or design writing, testing, maintenance, and why skipping steps causes rework
  - Outcome: the learner can list and apply the steps of the program development cycle

- [x] **Module 03: Algorithms and Precise Instructions**
  - Prerequisites: Modules 01 to 02
  - Teaches: what an algorithm is, properties of good algorithms, everyday examples, and turning a problem into ordered steps
  - Outcome: the learner can write a clear algorithm for a small problem

### Part 2: Designing solutions without a programming language

- [x] **Module 04: Writing Pseudocode**
  - Prerequisites: Modules 01 to 03
  - Teaches: pseudocode purpose, common keywords, indentation, input/output, and readable design style
  - Outcome: the learner can write pseudocode for a short sequential solution

- [x] **Module 05: Flowchart Symbols and Sequence Design**
  - Prerequisites: Modules 01 to 04
  - Teaches: terminal, process, input/output, decision, flow lines, connectors, and drawing a sequence flowchart that matches pseudocode
  - Outcome: the learner can draw and read a sequence flowchart

- [x] **Module 06: Variables, Constants, and Assignment**
  - Prerequisites: Modules 01 to 05
  - Teaches: named storage, constants, assignment, naming rules, data types at a conceptual level, and declaring vs using values
  - Outcome: the learner can design solutions that store and update named values

- [x] **Module 07: Arithmetic Operations and Expressions**
  - Prerequisites: Modules 01 to 06
  - Teaches: arithmetic operators, order of operations, expressions vs statements, integer vs real results conceptually, and clear formula design
  - Outcome: the learner can write correct arithmetic expressions in design form

- [x] **Module 08: Trace Tables and Desk Checking**
  - Prerequisites: Modules 01 to 07
  - Teaches: building a trace table, updating columns per step, finding logic mistakes before coding, and checking against expected results
  - Outcome: the learner can desk-check a sequential design with a trace table

### Part 3: Structure and modular design

- [x] **Module 09: Modules and Hierarchy Charts**
  - Prerequisites: Modules 01 to 08
  - Teaches: why programs are modularized, module headers, calling modules, passing data conceptually, and hierarchy charts
  - Outcome: the learner can split a solution into modules and show the hierarchy

- [x] **Module 10: Sequence, Selection, Loops, and Structured Design**
  - Prerequisites: Modules 01 to 09
  - Teaches: the three basic structures, spaghetti code, recognizing structure, and restructuring messy logic
  - Outcome: the learner can identify unstructured logic and redesign it with clear structures

### Part 4: Selection

- [x] **Module 11: Selection Structures and Boolean Expressions**
  - Prerequisites: Modules 01 to 10
  - Teaches: single-alternative and dual-alternative selection, boolean results, and flowchart diamonds for decisions
  - Outcome: the learner can design programs that choose one path based on a condition

- [x] **Module 12: Relational Operators and Logical Operators**
  - Prerequisites: Modules 01 to 11
  - Teaches: relational comparison operators, AND, OR, NOT, precedence, and truth evaluation
  - Outcome: the learner can evaluate and write compound conditions correctly

- [x] **Module 13: Range Checks and Nested Decisions**
  - Prerequisites: Modules 01 to 12
  - Teaches: range checks, multi-way selection, nesting decisions carefully, and keeping decision order correct
  - Outcome: the learner can design multi-branch and nested selection logic safely

### Part 5: Loops

- [x] **Module 14: Loop Structure and While Loops**
  - Prerequisites: Modules 01 to 13
  - Teaches: why loops matter, loop control variables, priming input, while-loop design, and avoiding infinite loops
  - Outcome: the learner can design a correct while loop with a clear termination condition

- [x] **Module 15: For Loops, Definite Loops, and Indefinite Loops**
  - Prerequisites: Modules 01 to 14
  - Teaches: definite vs indefinite loops, counted loops, for-loop design, and choosing while vs for
  - Outcome: the learner can choose and design the right loop form for a problem

- [x] **Module 16: Nested Loops, Mistakes, and Common Applications**
  - Prerequisites: Modules 01 to 15
  - Teaches: nested loops, common mistakes, accumulators, counters, sentinels, and everyday loop applications
  - Outcome: the learner can design nested loops and common loop patterns without control errors

### Part 6: Arrays

- [x] **Module 17: Arrays and How They Occupy Memory**
  - Prerequisites: Modules 01 to 16
  - Teaches: array purpose, size, indexes, contiguous storage idea, and reading or writing elements
  - Outcome: the learner can design solutions that store related values in arrays

- [x] **Module 18: Searching Arrays and Parallel Arrays**
  - Prerequisites: Modules 01 to 17
  - Teaches: linear search, found flags, parallel arrays, and replacing nested decisions with data lookup
  - Outcome: the learner can search arrays and keep related data aligned with parallel arrays

- [x] **Module 19: Processing Arrays with Loops**
  - Prerequisites: Modules 01 to 18
  - Teaches: for-loop array processing, totals, averages, min and max, and partial fills
  - Outcome: the learner can process every element of an array with a clear loop design

### Part 7: Python implementation and project work

- [x] **Module 20: Python Setup and First Programs**
  - Prerequisites: Modules 01 to 19
  - Teaches: what an IDE or editor is, installing or using an online Python environment, print, comments, running a script, and reading simple errors
  - Outcome: the learner can write and run a small Python program

- [x] **Module 21: Translating Design to Python Control Flow**
  - Prerequisites: Modules 01 to 20
  - Teaches: variables, assignment, arithmetic, input conversion, if and elif, while and for, and matching design to code
  - Outcome: the learner can convert sequential, selection, and loop designs into Python

- [x] **Module 22: Translating Modules and Arrays to Python**
  - Prerequisites: Modules 01 to 21
  - Teaches: functions as modules, parameters and return values at a practical level, lists as arrays, and full design-to-code translation
  - Outcome: the learner can implement modular, array-based designs in Python

- [x] **Module 23: Capstone Design and Build**
  - Prerequisites: Modules 01 to 22
  - Teaches: choosing a problem, writing requirements, producing pseudocode and flowchart, implementing in Python, testing with traces and runs, and presenting the result
  - Outcome: the learner completes one end-to-end programming concepts project

## Tools and practice media

- Paper or a simple drawing tool for flowcharts and hierarchy charts
- A text editor for pseudocode and Python
- An online Python environment or a local Python 3.12+ install for Modules 20 to 23
- No paid platform is required
- Optional game-based practice is not part of the required path

## Root README requirements

The course `README.md` must include:

1. a clear welcome for absolute beginners
2. what ProgCon is and is not
3. how to use each module
4. tools for design work and for Python practice
5. a routine for when designs or code fail
6. the full module map grouped by part
7. a suggested pace

## Root repository update

After the course is built, the main repository `README.md` should list `learn-to-progcon/` among the currently available courses, with a short description matching the other entries.

## Completion checks

A module is complete only when all five learning files exist, the lesson teaches only earlier and current ideas, the exercises are fully solvable from the lesson, the quiz stays inside the taught scope, and the answer files explain reasoning completely.

The course is complete when all 23 modules meet that standard and the course README presents a clear path from first concept to capstone project.
