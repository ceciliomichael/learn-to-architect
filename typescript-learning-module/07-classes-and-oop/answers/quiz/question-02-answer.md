# Question 02 Answer

**`this.engineCode` in `ElectricCar.switchFuel()`:**
BLOCKED. `engineCode` is `private`, which means it is only accessible inside the `Vehicle` class itself. Subclasses extending `Vehicle` cannot access `private` members.

**`this.fuelType` in `ElectricCar.switchFuel()`:**
ALLOWED. `fuelType` is `protected`, which means it is accessible inside `Vehicle` AND inside any class that extends `Vehicle`. `ElectricCar extends Vehicle`, so it has access.

**`car.engineCode` from outside the class:**
BLOCKED. `private` restricts access to the class it is declared in only. External code (including instances used outside the class) cannot access it.

**`car.fuelType` from outside the class:**
BLOCKED. `protected` restricts access to the declaring class and its subclasses. It does NOT allow access from arbitrary external code, even if you have a reference to the instance.

**When would you choose `protected` over `private`?**
When you are designing a base class that is meant to be extended, and the child classes need to read or modify the property as part of overriding behavior. A common example is a logging base class that stores a `protected serviceName`  -  child services inherit and use it in their `log()` implementations, but external code should never modify it.
