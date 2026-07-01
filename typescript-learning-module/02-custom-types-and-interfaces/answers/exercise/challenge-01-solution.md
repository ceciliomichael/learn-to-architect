# Challenge 01: Solution

```typescript
interface GameCharacter {
  readonly id: string;
  name: string;
  health: number;
  level: number;
  guild?: string;
  skills: string[];
}

const warrior: GameCharacter = {
  id: "char-001",
  name: "Aragorn",
  health: 250,
  level: 40,
  guild: "Rangers of the North",
  skills: ["Sword Mastery", "Tracking", "Leadership"]
};

const rogue: GameCharacter = {
  id: "char-002",
  name: "Shadowstep",
  health: 180,
  level: 35,
  // guild is omitted entirely  -  the '?' made it optional
  skills: ["Stealth", "Backstab", "Lockpicking"]
};

// warrior.id = "char-999";
// ERROR: Cannot assign to 'id' because it is a read-only property.
```
