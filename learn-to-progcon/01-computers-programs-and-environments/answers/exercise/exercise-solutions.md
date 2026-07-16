# Module 01 Exercise Solutions

Your examples can differ from these. The important part is correct use of the ideas: input, processing, output, storage, hardware, software, program, source instructions, results, and environments.

## Warm-up solution

Example task: looking up a product price online.

1. **Input**: the product name or product code the shopper types or scans.
2. **Processing**: the system finds the matching product record and reads its price.
3. **Output**: the price and product name appear on the screen.
4. **Storage**: product prices are kept in a product file or database so they do not need to be typed each time.

If you chose attendance, a strong answer mentions student identity as input, marking present/absent as processing, a list or confirmation as output, and the attendance record as storage.

## Guided exercise solution

1. **Hardware examples** (any three similar items are fine):
   - computer or laptop
   - keyboard
   - screen
   - printer

2. **Software examples** (any two similar items are fine):
   - operating system
   - student information application that builds schedules
   - printer driver software

3. **Program's job**:  
   The schedule program follows instructions that look up a student, gather their class list, arrange the times, and send the schedule to the screen or printer.

4. **Source instructions example**:

```text
1. Ask for the student ID.
2. Find the classes linked to that student ID.
3. Print the class names and meeting times.
```

5. **Result example**:  
   A printed page or on-screen list that shows period 1 Science, period 2 Math, and the rest of the day.

## Independent exercise solution

1. **Programming environment**  
   The designer or programmer works in a text editor or design notebook, writes the steps for reading prices and calculating totals, runs small tests, and reads error notes or failed check results. They care about clear instructions and correct math.

2. **User environment**  
   The shopper or cashier works at a phone, website, or register screen. They enter items or scan codes and need a total they trust. They care about speed, readable numbers, and a finished purchase, not about the source text.

3. **Comparison**

| Point | Programming environment | User environment |
| --- | --- | --- |
| Main person | Designer or programmer | Shopper or cashier |
| What is visible | Design steps, source text, tests, error messages | Buttons, prices, total, receipt |
| Main goal | Create and fix correct instructions | Complete a purchase with a correct total |

4. **Programming-environment mistake**  
   The instructions multiply tax twice, so every total is too high even though the screen looks professional.

5. **User-environment problem**  
   The total is calculated correctly, but the total is printed in tiny gray text on a bright screen, so people misread it during a busy checkout.

## Debugging / desk-check task solution

Corrected ideas:

1. **Original:** "The keyboard is software because it helps the user type."  
   **Problem:** A keyboard is a physical device.  
   **Better:** The keyboard is hardware. It is a physical input device.

2. **Original:** "The order program is hardware because it sits inside the computer."  
   **Problem:** A program is instructions, not a physical part.  
   **Better:** The order program is software. It is a set of instructions the computer follows.

3. **Original:** "Source instructions and results are the same thing: whatever appears on the screen."  
   **Problem:** Source instructions are what the writer creates. Results are produced when those instructions run.  
   **Better:** Source instructions describe the steps. Results are outputs such as a total shown on the screen.

4. **Original:** "Storage is optional because the total only needs to exist for one second."  
   **Problem:** Many systems must keep records. Even short tasks often need memory while they run.  
   **Better:** Storage matters. Memory holds values while the program runs, and sales records are often saved for later review.

5. **Original:** "A programming environment is where customers pay for coffee."  
   **Problem:** That describes a user environment.  
   **Better:** Customers pay in a user environment. A programming environment is where people write, check, and test the instructions.

Full corrected paragraph:

```text
The keyboard is hardware used for input.
The order program is software: instructions the computer follows.
Source instructions are the written steps or code. Results are outputs such as totals on the screen.
Storage holds data in memory while the program runs and can save records for later.
Customers pay in a user environment. Developers write and test instructions in a programming environment.
```
