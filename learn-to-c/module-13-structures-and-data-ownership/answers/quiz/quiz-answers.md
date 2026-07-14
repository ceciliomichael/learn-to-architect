# Quiz Answers: Structures and Data Ownership

1. **What does structure assignment copy?**

   It copies each field value, including every element of embedded arrays and the address value of each pointer field.

2. **Does copying a pointer field copy its target?**

   No. It creates another pointer value designating the same target.

3. **When is the arrow operator used?**

   It selects a field through a pointer to a structure.

4. **Why must an API document pointer ownership?**

   The C pointer type alone does not say who keeps the target alive or who releases it.

5. **What is a designated initializer useful for?**

   It names each initialized field, making intent clear and reducing dependence on field order.

