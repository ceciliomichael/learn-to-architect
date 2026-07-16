# Module 09 Exercise Solutions

## Warm-up solution

One clean split:

```text
                    Main
                      |
     -----------------+-----------------
     |          |           |          |
DisplayWelcome GetOrder  CalcLineTotal DisplayLineTotal
                                   |
                              (optional goodbye under Main)
```

A full chart with goodbye:

```text
                         Main
                           |
     ----------------------+----------------------
     |           |         |          |          |
DisplayWelcome GetOrder CalcLineTotal DisplayLineTotal DisplayGoodbye
```

Main:

```text
Module Main
    Call DisplayWelcome
    Call GetOrder
    Call CalcLineTotal
    Call DisplayLineTotal
    Call DisplayGoodbye
End Module
```

Job descriptions:

- `DisplayWelcome`: show the opening message
- `GetOrder`: collect pastry name, unit price, and quantity
- `CalcLineTotal`: compute price times quantity
- `DisplayLineTotal`: show the calculated amount
- `DisplayGoodbye`: show the closing message

Other valid splits exist. For example, display of the line total could stay inside a larger output module if the module still has one clear reporting job.

## Guided exercise solution

### Hierarchy chart

```text
                              Main
                                |
        ------------------------+------------------------
        |            |          |           |           |
DisplayWelcome GetRoomData CalcOccupancy DisplayOccupancy DisplayThanks
```

### Main

```text
Module Main
    Declare Integer totalSeats
    Declare Integer filledSeats
    Declare Integer emptySeats
    Declare Real percentFull

    Call DisplayWelcome
    Call GetRoomData(totalSeats, filledSeats)
    Call CalcOccupancy(totalSeats, filledSeats, emptySeats, percentFull)
    Call DisplayOccupancy(emptySeats, percentFull)
    Call DisplayThanks
End Module
```

### Modules

```text
Module DisplayWelcome
    Display "Welcome to the room occupancy helper."
End Module

Module GetRoomData(totalSeats, filledSeats)
    Display "Enter total seats: "
    Input totalSeats
    Display "Enter seats currently filled: "
    Input filledSeats
End Module

Module CalcOccupancy(totalSeats, filledSeats, emptySeats, percentFull)
    Set emptySeats = totalSeats - filledSeats
    Set percentFull = (filledSeats / totalSeats) * 100
End Module

Module DisplayOccupancy(emptySeats, percentFull)
    Display "Empty seats: ", emptySeats
    Display "Percent full: ", percentFull
End Module

Module DisplayThanks
    Display "Thank you."
End Module
```

### Data notes

- `GetRoomData` produces `totalSeats` and `filledSeats`.
- `CalcOccupancy` needs those counts and produces `emptySeats` and `percentFull`.
- `DisplayOccupancy` needs the calculated results only.

Sample desk check: total 40, filled 30.

- empty seats = 10
- percent full = 75

## Independent exercise solution

### Hierarchy chart

```text
                                Main
                                  |
      ----------------------------+----------------------------
      |            |              |             |             |
DisplayWelcome GetStudentOrder CalcPurchase DisplayReceipt DisplayGoodbye
```

### Pseudocode

```text
Module Main
    Declare String studentName
    Declare String itemName
    Declare Real price
    Declare Integer quantity
    Declare Real subtotal
    Declare Real tax
    Declare Real grandTotal

    Call DisplayWelcome
    Call GetStudentOrder(studentName, itemName, price, quantity)
    Call CalcPurchase(price, quantity, subtotal, tax, grandTotal)
    Call DisplayReceipt(studentName, itemName, quantity, subtotal, tax, grandTotal)
    Call DisplayGoodbye
End Module

Module DisplayWelcome
    Display "Campus Supply Desk"
End Module

Module GetStudentOrder(studentName, itemName, price, quantity)
    Display "Enter student name: "
    Input studentName
    Display "Enter item name: "
    Input itemName
    Display "Enter item price: "
    Input price
    Display "Enter quantity: "
    Input quantity
End Module

Module CalcPurchase(price, quantity, subtotal, tax, grandTotal)
    Set subtotal = price * quantity
    Set tax = subtotal * 0.05
    Set grandTotal = subtotal + tax
End Module

Module DisplayReceipt(studentName, itemName, quantity, subtotal, tax, grandTotal)
    Display "Student: ", studentName
    Display "Item: ", itemName
    Display "Quantity: ", quantity
    Display "Subtotal: ", subtotal
    Display "Tax: ", tax
    Display "Grand total: ", grandTotal
End Module

Module DisplayGoodbye
    Display "Have a great day."
End Module
```

### Why this split is better

Main shows the story of a checkout in five clear calls. Input, calculation, and receipt display can change independently. If the tax rate changes, you edit `CalcPurchase` without rewriting the welcome message or the prompt text. The hierarchy chart makes the structure easy to explain to another person.

Sample values: price 2.00, quantity 4.

- subtotal = 8.00
- tax = 0.40
- grand total = 8.40

## Debugging and desk-check task solution

### Problems in the original design

1. Call order is wrong. `DisplayTotal` runs before price is entered and before total is calculated.
2. `DisplayTotal` needs `total`, but `total` is not created until `CalculateTotal`.
3. `CalculateTotal` needs `price`, which is fine only if `GetPrice` runs first.
4. Data dependencies are hidden because modules share names without clear parameters.

### Corrected design

```text
Module Main
    Declare Real price
    Declare Real total

    Call DisplayWelcome
    Call GetPrice(price)
    Call CalculateTotal(price, total)
    Call DisplayTotal(total)
End Module

Module DisplayWelcome
    Display "Welcome"
End Module

Module GetPrice(price)
    Display "Enter price: "
    Input price
End Module

Module CalculateTotal(price, total)
    Set total = price * 1.08
End Module

Module DisplayTotal(total)
    Display "Total is ", total
End Module
```

### Desk check with price = 50

| Step | price | total | Notes |
| --- | --- | --- | --- |
| After GetPrice | 50 | (none yet) | Input stored |
| After CalculateTotal | 50 | 54 | 50 * 1.08 |
| DisplayTotal | 50 | 54 | Shows 54 |

Expected displayed total: **54**

Reasoning: the tax-inclusive multiplier 1.08 means an 8 percent addition. 50 * 1.08 = 54.
