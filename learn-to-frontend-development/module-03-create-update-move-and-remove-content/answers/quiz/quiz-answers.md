# Quiz Answers: Create, Update, Move, and Remove Content

1. **Why prefer textContent for ordinary text?**

   It inserts text without parsing it as markup.

2. **What happens when an existing node is appended elsewhere?**

   It moves from its old parent rather than being copied.

3. **How is a copy created?**

   Create a new node or deliberately clone one, then repair any ids and state.

4. **Why update a small region?**

   It preserves unrelated focus, selection, media, and browser state.

5. **What must be considered before remove?**

   Focus, listener ownership, references, and whether the user can recover the removed data.

