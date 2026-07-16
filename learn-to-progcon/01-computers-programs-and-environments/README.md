# Module 01: Computers, Programs, and Environments

## Before you start

You do not need any programming knowledge for this module.

You only need curiosity about how a computer turns a request into a result. Paper and a pen help if you want to sketch the diagrams.

## What you will learn

By the end of this module, you will be able to:

- name the four main parts of a computer system: input, processing, output, and storage
- tell hardware apart from software
- explain what a program is in plain words
- separate source instructions from the results they produce
- contrast a programming environment with a user environment
- say why the tools you use matter when you learn to design and build programs

## Why this matters

People often say "the computer did it" as if the machine invents its own plans. A computer only follows instructions that someone wrote earlier. If you understand what a computer is, what a program is, and where you write those instructions, the rest of this course has a solid foundation.

## 1. What a computer system does

A **computer** is a machine that accepts data, works on that data according to instructions, and produces results. A **computer system** is the whole set of parts that make this possible: devices you can touch, programs you cannot touch, and the data that moves through both.

Almost every computer task can be described with four ideas:

1. **Input**: information that comes into the system
2. **Processing**: the work done to that information
3. **Output**: information that goes out of the system
4. **Storage**: places where information is kept for later use

These four ideas form a simple model of what a computer system does.

```text
  Input  --->  Processing  --->  Output
                  |
                  v
               Storage
```

### Everyday example: checking a grade average

Imagine a student opens a grades app and asks for their average.

1. **Input**: the student taps "Show average," and the system already has stored scores such as 88, 92, and 85.
2. **Processing**: the system adds the scores and divides by the number of scores.
3. **Output**: the screen shows `88.3` (or a rounded value).
4. **Storage**: the scores and the average can be saved so the student can open them again later.

The same four parts appear when you buy a product online, check a bus schedule, or convert a temperature from Celsius to Fahrenheit.

### Another example: a store price calculator

A clerk enters a shirt price of `20.00` and a tax rate of `8%`.

1. **Input**: price and tax rate
2. **Processing**: multiply price by tax rate, then add tax to price
3. **Output**: total due of `21.60`
4. **Storage**: the sale record may be saved in a sales file

You do not need to know electronics to use this model. You only need to ask: what comes in, what work is done, what comes out, and what is saved.

## 2. Input, processing, output, and storage in more detail

### Input

**Input** is any data or signal that enters the computer system. Common input devices include:

- keyboard
- mouse or trackpad
- touchscreen
- microphone
- camera
- barcode scanner

Input can also come from a file, a network message, or a sensor. The important idea is direction: information is coming *into* the system.

Example input values:

- a customer name: `Amina`
- a temperature reading: `72`
- a yes/no answer: `Y`
- a list of attendance marks: present or absent

### Processing

**Processing** is the work the computer performs on input. The part of the machine that does most of this work is the **CPU** (central processing unit). You can think of the CPU as the place that follows the current instructions.

Processing includes:

- calculating totals and averages
- comparing values (is the score above 70?)
- rearranging data
- deciding which message to show
- preparing a result for display or storage

Processing does not invent goals. It follows the instructions in a program.

### Output

**Output** is any result that leaves the system for a person or another device. Common output devices include:

- screen or monitor
- printer
- speakers
- projector

Output can also be a file written to a disk, a message sent over a network, or a signal to a machine.

Example outputs:

- a message: `Payment received`
- a number: `21.60`
- a report of who attended class today
- a sound that means "error"

### Storage

**Storage** holds data and instructions so they can be used later. Two broad kinds matter:

- **Primary storage** (memory, often called RAM): fast storage used while programs run. When the computer powers off, this temporary memory usually loses its contents.
- **Secondary storage** (disk drive, solid-state drive, USB stick, cloud storage): slower than RAM for many tasks, but it keeps information after the computer is turned off.

Programs and data need storage. Without storage, every program would vanish when you closed it, and every grade list would have to be typed again from scratch.

## 3. Hardware versus software

**Hardware** is the physical parts of a computer system. You can point at hardware. Examples:

- keyboard
- screen
- CPU chip
- memory modules
- disk drive
- printer
- cables

**Software** is the set of instructions and related data that tell the hardware what to do. You cannot hold software in your hand the way you hold a keyboard. Examples:

- an operating system such as Windows, macOS, or Linux
- a web browser
- a word processor
- a calculator app
- a grades program
- the designs and code you will write later in this course

Hardware without software is like a blank notebook with no writing. Software without hardware has nowhere to run.

### System software and application software

Software is often grouped into two large families:

1. **System software** manages the computer itself. The operating system is the main example. It starts the machine, manages files, and helps other programs run.
2. **Application software** helps a person complete a task. Examples include a shopping app, a spreadsheet, a music player, and a classroom attendance tool.

When you use a browser to check prices, the browser is application software. The operating system under it is system software. Both depend on hardware.

### Predict the result

Label each item as hardware or software:

1. a laptop screen
2. a free note-taking app
3. a USB flash drive
4. an operating system update
5. a classroom projector

Answers: 1 hardware, 2 software, 3 hardware, 4 software, 5 hardware.

## 4. What a program is

A **program** is a set of instructions that a computer can follow to complete a task.

Those instructions must be written in a form the computer's tools can accept. Humans invent **programming languages** so people can write instructions with clear rules. Later modules teach design tools that sit *before* a full programming language. For now, hold this simple picture:

```text
Problem to solve
      |
      v
Instructions written by a person
      |
      v
Tools prepare or translate those instructions
      |
      v
Computer hardware carries them out
      |
      v
Results (output, stored data, or both)
```

### A tiny program idea (no code required yet)

Task: greet a shopper by name.

Intended steps:

1. Ask for the shopper's name.
2. Store that name.
3. Show the message `Hello,` followed by the name.

If the shopper types `Jordan`, the result should be something like:

```text
Hello, Jordan
```

That sequence of instructions is a program idea. When it is written in a real programming language and run on a machine, it becomes a running program.

### Programs are not magic

A program cannot "know" your goal unless the instructions say so. If the instructions forget to show the greeting, no greeting appears. If the instructions add tax twice, the total is wrong. Good results come from clear instructions plus careful checking.

## 5. Source instructions versus results

It is easy to confuse what a person writes with what a user sees. These are different things.

**Source instructions** (often called **source code** when written in a programming language) are the text a person creates to describe the solution. They may include special words, punctuation, and structure that tools need.

**Results** are what appear when the instructions are carried out. Results may be text on a screen, a printed receipt, a saved file, or a chart.

### Side-by-side example

Source instructions (plain design form, not a full language yet):

```text
1. Ask for the item price.
2. Ask for the tax rate.
3. Multiply price by tax rate to get tax amount.
4. Add price and tax amount to get total.
5. Show the total.
```

If the price is `10.00` and the tax rate is `0.05`, one correct result is:

```text
10.50
```

Notice:

- The numbered steps are instructions.
- `10.50` is a result.
- The words "Ask," "Multiply," and "Show" are part of the design. They are not what the customer needs to see on a receipt, unless the design says so.

### Why this separation matters

When something goes wrong, ask:

1. Is the problem in the instructions?
2. Or is the problem only in how you are reading the results?

If the total is wrong, the instructions or the input values may be wrong. If the total is right but a person expected a different message format, the result display may need a clearer design. Separating source from results makes troubleshooting calmer and faster.

## 6. Programming environment versus user environment

An **environment**, in everyday language, is the setting where work happens. In computing, people use the word for the tools and conditions around a program.

### Programming environment

A **programming environment** is the set of tools a person uses to write, check, and run instructions. It may include:

- a text editor or IDE (integrated development environment)
- a way to run or test a program
- error messages that point to problems in the instructions
- folders for project files
- optional drawing tools for designs and diagrams

In this course, your early programming environment is simple: paper or a text editor for designs, then later a Python environment for running code. You do not need a complex setup for Modules 01 to 19.

### User environment

A **user environment** is the setting where a person *uses* a finished program. It may include:

- a phone app screen
- a website in a browser
- a point-of-sale terminal in a shop
- a shared computer in a classroom

The user usually does not see the source instructions. The user sees buttons, forms, messages, and results.

### Compare the two

| Question | Programming environment | User environment |
| --- | --- | --- |
| Who is the main person? | The person writing or fixing instructions | The person completing a task with the program |
| What is visible? | Source text, design notes, error reports | Screens, reports, sounds, saved files |
| Main goal | Create correct instructions | Complete a job such as buying, learning, or recording attendance |
| Example | Editing steps for a grade calculator | A student viewing their average |

A helpful habit: when you design a solution, think like both people. Write instructions that a computer (and your later self) can follow. Also imagine the person who only wants a clear total or a clear message.

## 7. Why tools matter

Tools do not replace thinking. Tools support thinking.

Useful tools help you:

- write instructions so they stay readable
- find spelling or structure mistakes early
- redraw a design when the plan changes
- keep versions of your work
- run small tests when you reach a programming language

Poor tools, or no tools, slow you down:

- messy notes that only you understand for one day
- lost files
- designs that skip steps because nothing forced you to write them down
- results you cannot reproduce

### Good beginner tool habits

1. Keep designs in one place (a notebook section or a folder).
2. Write the problem in one sentence before you write steps.
3. Number your steps.
4. Check a small example by hand (desk checking, which later modules teach in depth).
5. Change one thing at a time when a result is wrong.

You do not need expensive software to learn programming concepts. Clear writing and careful checking matter more than a fancy editor at this stage.

## 8. Putting the pieces together

Here is one full walk-through that uses every main idea from this module.

**Scene:** A cafe wants a simple total for a drink order.

1. **Hardware**: keyboard, screen, computer under the counter.
2. **Software**: a small order program running on that computer.
3. **Input**: drink price `4.50`, quantity `2`.
4. **Processing**: multiply `4.50` by `2` to get `9.00`.
5. **Output**: show `Total: 9.00` on the screen.
6. **Storage**: save the sale so the owner can review daily totals later.
7. **Source instructions**: the written steps or code that define how totals are calculated.
8. **Results**: the total the clerk and customer see.
9. **Programming environment**: where the cafe's program was written and tested.
10. **User environment**: the counter screen the clerk uses during a rush.

If the total is wrong, the clerk does not need to understand every chip inside the machine. The designer or programmer must re-check the instructions, the input values, and the tests.

## Common mistakes

### Treating the computer as if it understands wishes

The machine follows instructions. It does not guess what you meant. Vague wishes lead to vague results.

### Mixing up hardware and software problems

A broken cable is a hardware problem. A wrong formula in a program is a software problem. Naming the kind of problem helps you fix the right thing.

### Confusing source instructions with output

If someone asks "What does the program say?", they may mean the source text or the on-screen result. Be specific.

### Ignoring storage

People design a process that works once, then forget that data must be saved. Ask early: what must remain after the program closes?

### Designing only for yourself as the programmer

A design that only makes sense in your head is hard to test and hard to improve. Write steps another careful reader could follow.

## Check your understanding

1. Name the four main parts of the computer system model used in this lesson.
2. Is a keyboard hardware or software? Is a browser hardware or software?
3. In one sentence, what is a program?
4. What is the difference between source instructions and results?
5. How is a programming environment different from a user environment?
6. Why do tools matter even when you are only writing designs on paper?

## Practice

Complete the [module exercises](./exercise/exercise.md). Write your answers carefully. Then take the [module quiz](./quiz/quiz.md).

## Next step

In [Module 02](../02-problem-solving-and-the-program-development-cycle/README.md), you will learn a repeatable cycle for solving problems with programs: understand, plan, write, test, and maintain.
